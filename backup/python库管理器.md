# python库管理器
## 下载链接

> 主链接：https://www.123865.com/s/SsSejv-3EYgh
备用链接https://www.123684.com/s/SsSejv-3EYgh
提取码`ikNB`
## 源代码
作者：ikdxhz
```python
#作者：ikdxhz
#未经授权或非作者二改或倒卖死女马
#作者：ikdxhz
#未经授权或非作者二改或倒卖死女马
#作者：ikdxhz
#未经授权或非作者二改或倒卖死女马
#重要的事情说三遍
#可以用于学习研究
import subprocess
import sys
import re
import json
import requests
from socket import gethostbyname, gaierror
import logging
from datetime import datetime

logging.basicConfig(filename='library_manager.log', level=logging.INFO,
                    format='%(asctime)s - %(levelname)s - %(message)s')

print("作者: ikdxhz")

pip_source = []

PIP_SOURCES = {
    "aliyun": "https://mirrors.aliyun.com/pypi/simple/",
    "tsinghua": "https://pypi.tuna.tsinghua.edu.cn/simple/",
    "douban": "https://pypi.douban.com/simple/",
    "ustc": "https://pypi.mirrors.ustc.edu.cn/simple/",
    "default": ""
}

def check_python_version():
    major, minor, micro, releaselevel, serial = sys.version_info
    if major < 3 or (major == 3 and minor < 6) or (major == 3 and minor == 6 and micro < 1):
        print(f"当前Python版本为 {sys.version}, 脚本需要Python 3.6.1或更高版本.")
        logging.error(f"不支持的Python版本: {sys.version}")
        sys.exit(1)
    else:
        print(f"当前Python版本为 {sys.version}, 符合要求.")
        logging.info(f"支持的Python版本: {sys.version}")

def check_pip_installed():
    try:
        subprocess.check_call([sys.executable, '-m', 'pip', '--version'])
        return True
    except subprocess.CalledProcessError:
        print("未找到pip，请确保pip已安装并添加到PATH中.")
        logging.error("未找到pip")
        return False

def set_pip_source(source):
    global pip_source
    if source in PIP_SOURCES:
        pip_source = ["-i", PIP_SOURCES[source]] if PIP_SOURCES[source] else []
        print(f"已切换到 {source} 源.")
        logging.info(f"切换到 {source} 源")
        return True
    else:
        print("无效的源选择，请输入 aliyun, tsinghua, douban, ustc 或 default.")
        logging.warning(f"无效的源选择: {source}")
        return False

def get_current_source():
    for key, value in PIP_SOURCES.items():
        if pip_source == ["-i", value]:
            return key
    return "default"

def get_pip_command():
    commands_to_try = ['pip', 'pip3']
    for cmd in commands_to_try:
        try:
            subprocess.check_call([cmd, '--version'])
            return [cmd]
        except FileNotFoundError:
            continue
    
    retries = 3
    while retries > 0:
        manual_input = input("未找到pip或pip3，请手动输入pip命令 (例如 'pip' 或 'pip3')，或输入 'exit' 退出: ").strip()
        if manual_input.lower() == 'exit':
            print("退出程序.")
            logging.info("用户选择退出程序")
            sys.exit(1)
        try:
            subprocess.check_call([manual_input, '--version'])
            return [manual_input]
        except FileNotFoundError:
            retries -= 1
            print(f"手动输入的pip命令无效，请重新输入 ({retries} 次尝试剩余).")
    
    print("多次尝试无效，请确保pip已安装并添加到PATH中。你可以通过以下命令安装pip:")
    print("curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py && python get-pip.py")
    logging.error("多次尝试无效，未找到有效的pip命令")
    sys.exit(1)

def run_pip_command(pip_command, command, args=[]):
    full_command = pip_command + command + args + pip_source
    try:
        result = subprocess.run(full_command, capture_output=True, text=True, check=True)
        logging.info(f"成功执行命令: {' '.join(full_command)}")
        return True
    except subprocess.CalledProcessError as e:
        print(f"\n命令 {' '.join(full_command)} 失败:")
        print(e.stderr.strip())
        logging.error(f"命令执行失败: {' '.join(full_command)}, 错误: {e.stderr.strip()}")
        return False
    except FileNotFoundError:
        print(f"\n命令 {' '.join(full_command)} 找不到文件.")
        logging.error(f"命令找不到文件: {' '.join(full_command)}")
        return False
    except Exception as e:
        print(f"发生未知错误: {e}")
        logging.error(f"发生未知错误: {e}")
        return False

def install(pip_command, package):
    if run_pip_command(pip_command, ['install'], [package]):
        print(f"\n{package} 安装成功.")
        logging.info(f"{package} 安装成功")
    else:
        print(f"\n{package} 安装失败.")
        suggest_similar_packages(pip_command, package)
        logging.warning(f"{package} 安装失败")

def update_single(pip_command, package):
    if run_pip_command(pip_command, ['install', '--upgrade'], [package]):
        print(f"\n{package} 更新成功.")
        logging.info(f"{package} 更新成功")
    else:
        print(f"\n{package} 更新失败.")
        suggest_similar_packages(pip_command, package)
        logging.warning(f"{package} 更新失败")

def update_all(pip_command):
    try:
        result = subprocess.run(pip_command + ['list', '--outdated', '--format=json'] + pip_source, capture_output=True, text=True, check=True)
        outdated_packages = json.loads(result.stdout)
        
        if isinstance(outdated_packages, list):
            packages = outdated_packages
        elif isinstance(outdated_packages, dict) and 'packages' in outdated_packages:
            packages = outdated_packages['packages'].values()
        else:
            print("\n解析后的JSON数据格式不正确.")
            logging.warning("解析后的JSON数据格式不正确")
            list_all_packages(pip_command)
            return
        
        if not packages:
            print("\n没有可更新的库.")
            logging.info("没有可更新的库")
            list_all_packages(pip_command)
            return
        
        for package in packages:
            if not isinstance(package, dict) or 'name' not in package or 'latest_version' not in package:
                print(f"\n包信息不完整: {package}")
                logging.warning(f"包信息不完整: {package}")
                continue
            
            package_name = package['name']
            latest_version = package['latest_version']
            if run_pip_command(pip_command, ['install', '--upgrade'], [package_name]):
                print(f"{package_name} 更新成功. 新版本: {latest_version}.")
                logging.info(f"{package_name} 更新成功, 新版本: {latest_version}")
            else:
                print(f"{package_name} 更新失败.")
                logging.warning(f"{package_name} 更新失败")
    except subprocess.CalledProcessError as e:
        print(f"\n获取过时库列表失败: {e.stderr.strip()}")
        logging.error(f"获取过时库列表失败: {e.stderr.strip()}")
    except json.JSONDecodeError as e:
        print(f"\n解析JSON数据失败: {e}")
        logging.error(f"解析JSON数据失败: {e}")
    except Exception as e:
        print(f"发生未知错误: {e}")
        logging.error(f"发生未知错误: {e}")

def uninstall(pip_command, package):
    try:
        result = subprocess.run(pip_command + ['show', package], capture_output=True, text=True, check=True)
        dependencies = re.findall(r'Requires:\s*(.*)', result.stdout)
        if dependencies:
            print(f"\n警告: {package} 被以下包依赖: {dependencies[0]}")
            logging.warning(f"{package} 被以下包依赖: {dependencies[0]}")
            confirm = input("确定要卸载吗? (y/n): ").strip().lower()
            if confirm != 'y':
                print("取消卸载.")
                logging.info(f"用户取消卸载 {package}")
                return
        else:
            print(f"\n{package} 没有被其他包依赖.")
            logging.info(f"{package} 没有被其他包依赖")
        
        if run_pip_command(pip_command, ['uninstall', '-y'], [package]):
            print(f"\n{package} 卸载成功.")
            logging.info(f"{package} 卸载成功")
        else:
            print(f"\n{package} 卸载失败.")#ikdxhz
            print("请检查以下几点:")#ikdxhz
            print("1. 确保你有足够的权限来卸载该包.")#ikdxhz
            print("2. 检查是否有其他包依赖于该包.")#ikdxhz
            print("3. 尝试手动卸载该包，使用命令: pip uninstall -y {package}")#ikdxhz
            logging.warning(f"{package} 卸载失败")#ikdxhz
    except subprocess.CalledProcessError as e:
        print(f"\n获取包信息失败: {e.stderr.strip()}")
        logging.error(f"获取包信息失败: {e.stderr.strip()}")
    except Exception as e:
        print(f"发生未知错误: {e}")
        logging.error(f"发生未知错误: {e}")

def list_all_packages(pip_command):
    try:
        result = subprocess.run(pip_command + ['list', '--format=columns'] + pip_source, capture_output=True, text=True, check=True)
        print("\n已安装的库:")
        print(result.stdout)
        logging.info("列出所有库")
    except subprocess.CalledProcessError as e:
        print(f"\n列出已安装库失败: {e.stderr.strip()}")
        logging.error(f"列出已安装库失败: {e.stderr.strip()}")
    except Exception as e:
        print(f"发生未知错误: {e}")
        logging.error(f"发生未知错误: {e}")

def get_valid_package_name(prompt):
    while True:
        package_name = input(prompt).strip()
        if package_name:
            if re.match(r'^[A-Za-z0-9_\-\.]+$', package_name):
                return package_name
            else:
                print("无效的库名格式，请重新输入.")
        else:
            print("库名不能为空，请重新输入.")

def suggest_similar_packages(pip_command, package_name):
    try:
        result = subprocess.run(pip_command + ['search', package_name], capture_output=True, text=True, check=True)
        suggestions = result.stdout.splitlines()
        if suggestions:
            print("\n可能你想安装的是以下包之一:")
            for suggestion in suggestions[:5]:
                print(suggestion)
        else:
            print("\n没有找到类似的包.")
        logging.info(f"建议相似包: {package_name}")
    except subprocess.CalledProcessError as e:
        print(f"\n搜索类似包失败: {e.stderr.strip()}")
        logging.error(f"搜索类似包失败: {e.stderr.strip()}")
    except Exception as e:
        print(f"发生未知错误: {e}")
        logging.error(f"发生未知错误: {e}")

def get_random_hitokoto():
    url = "https://api.52vmy.cn/api/wl/yan/yiyan"
    try:
        response = requests.get(url, timeout=5)
        response.raise_for_status()
        data = response.json()
        if data["code"] == 200:
            hitokoto = data["data"]["hitokoto"]
            print(hitokoto)
            logging.info(f"随机一言: {hitokoto}")
        else:
            print("\n获取随机一言失败.")
            logging.warning("获取随机一言失败")
    except requests.HTTPError as http_err:
        print(f"\nHTTP 错误: {http_err}")
        logging.error(f"HTTP 错误: {http_err}")
    except requests.ConnectionError as conn_err:
        print(f"\n连接错误: {conn_err}")
        logging.error(f"连接错误: {conn_err}")
    except requests.Timeout as timeout_err:
        print(f"\n请求超时: {timeout_err}")
        logging.error(f"请求超时: {timeout_err}")
    except requests.RequestException as req_err:
        print(f"\n请求失败: {req_err}")
        logging.error(f"请求失败: {req_err}")
    except json.JSONDecodeError as json_err:
        print(f"\nJSON解码错误: {json_err}")
        logging.error(f"JSON解码错误: {json_err}")
    except Exception as e:
        print(f"发生未知错误: {e}")
        logging.error(f"发生未知错误: {e}")

def get_weather(ip=None):
    url = "https://api.52vmy.cn/api/query/tian"
    params = {}
    if ip:
        params["ip"] = ip
    
    try:
        response = requests.get(url, params=params, timeout=5)
        response.raise_for_status()
        data = response.json()
        if data["code"] == 200:
            weather_data = data["data"].get('current', {})
            print("\n天气信息:")
            if city := weather_data.get('city'):
                print(f"城市: {city}")
            if weather := weather_data.get('weather'):
                print(f"天气: {weather}")
            if temp := weather_data.get('temp'):
                print(f"温度: {temp}°C")
            if max_degree := weather_data.get('max_degree'):
                print(f"最高温度: {max_degree}°C")
            if min_degree := weather_data.get('min_degree'):
                print(f"最低温度: {min_degree}°C")
            if windn := weather_data.get('windn'):
                print(f"风向: {windn}")
            if windr := weather_data.get('windr'):
                print(f"风力: {windr}")
            if humidity := weather_data.get('humidity'):
                print(f"湿度: {humidity}%")
            if precipitation := weather_data.get('precipitation'):
                print(f"降水概率: {precipitation}%")
            if pressure := weather_data.get('pressure'):
                print(f"气压: {pressure} hPa")
            if sunup := weather_data.get('sunup'):
                print(f"日出时间: {sunup}")
            if sunset := weather_data.get('sunset'):
                print(f"日落时间: {sunset}")
            if tips := data.get('tips'):
                print(f"提示语: {tips}\n")
            logging.info(f"天气信息: {weather_data}")
        else:
            print(f"\n获取天气信息失败: {data.get('msg', '未知错误')}")
            logging.warning(f"获取天气信息失败: {data.get('msg', '未知错误')}")
    except requests.HTTPError as http_err:
        print(f"\nHTTP 错误: {http_err}")
        logging.error(f"HTTP 错误: {http_err}")
    except requests.ConnectionError as conn_err:
        print(f"\n连接错误: {conn_err}")
        logging.error(f"连接错误: {conn_err}")
    except requests.Timeout as timeout_err:
        print(f"\n请求超时: {timeout_err}")
        logging.error(f"请求超时: {timeout_err}")
    except requests.RequestException as req_err:
        print(f"\n请求失败: {req_err}")
        logging.error(f"请求失败: {req_err}")
    except json.JSONDecodeError as json_err:
        print(f"\nJSON解码错误: {json_err}")
        logging.error(f"JSON解码错误: {json_err}")
    except Exception as e:
        print(f"发生未知错误: {e}")
        logging.error(f"发生未知错误: {e}")

def check_network_connection():
    try:
        host = "8.8.8.8"
        gethostbyname(host)
        return True
    except gaierror:
        print("无法连接到互联网，请检查您的网络连接.")
        logging.error("无法连接到互联网")
        return False

def main():
    current_source = get_current_source()
    print(f"\n当前使用的pip源: {current_source}\n")
    logging.info(f"当前使用的pip源: {current_source}")
    
    if check_network_connection():
        get_random_hitokoto()
        get_weather()
    
    print("\nikdxhz出品，必属精品")
    
    while True:
        get_random_hitokoto()
        print("\n请选择操作:")
        print("1. 切换pip源")
        print("2. 安装库")
        print("3. 更新单个库")
        print("4. 更新所有库")
        print("5. 卸载库")
        print("6. 列出所有库")
        print("7. 退出")
        
        choice = input("请输入选项 (1/2/3/4/5/6/7): ").strip()
        
        if choice == "7":
            print("退出程序.")
            logging.info("用户选择退出程序")
            break
        
        if choice == "1":
            print("\n请选择pip源:")
            print("1. 阿里云")
            print("2. 清华大学")
            print("3. 豆瓣")
            print("4. 中国科学技术大学")
            print("5. 默认源")
            
            source_choice = input("请输入源编号 (1/2/3/4/5): ").strip()
            
            if source_choice == "1":
                if set_pip_source("aliyun"):
                    current_source = get_current_source()
                    print(f"当前使用的pip源: {current_source}\n")
                    logging.info(f"当前使用的pip源: {current_source}")
            elif source_choice == "2":
                if set_pip_source("tsinghua"):
                    current_source = get_current_source()
                    print(f"当前使用的pip源: {current_source}\n")
                    logging.info(f"当前使用的pip源: {current_source}")
            elif source_choice == "3":
                if set_pip_source("douban"):
                    current_source = get_current_source()
                    print(f"当前使用的pip源: {current_source}\n")
                    logging.info(f"当前使用的pip源: {current_source}")
            elif source_choice == "4":
                if set_pip_source("ustc"):
                    current_source = get_current_source()
                    print(f"当前使用的pip源: {current_source}\n")
                    logging.info(f"当前使用的pip源: {current_source}")
            elif source_choice == "5":
                if set_pip_source("default"):
                    current_source = get_current_source()
                    print(f"当前使用的pip源: {current_source}\n")
                    logging.info(f"当前使用的pip源: {current_source}")
            else:
                print("无效的选择，请输入 1, 2, 3, 4 或 5.")
                logging.warning(f"无效的源选择: {source_choice}")
        
        elif choice in ["2", "3", "5"]:
            package_name = get_valid_package_name("请输入库名: ")
            
            if choice == "2":
                install(pip_command, package_name)
            elif choice == "3":
                update_single(pip_command, package_name)
            elif choice == "5":
                uninstall(pip_command, package_name)
        
        elif choice == "4":
            update_all(pip_command)
        
        elif choice == "6":
            list_all_packages(pip_command)
        
        else:
            print("无效的选择，请输入 1, 2, 3, 4, 5, 6 或 7.")
            logging.warning(f"无效的选择: {choice}")

if __name__ == "__main__":
    check_python_version()
    try:
        import requests
    except ImportError:
        print("缺少requests库，请先安装requests库: pip install requests")
        logging.error("缺少requests库")
        sys.exit(1)
    
    start_time = datetime.now()
    logging.info(f"程序启动时间: {start_time}")
    pip_command = get_pip_command()
    main()
    end_time = datetime.now()
    logging.info(f"程序结束时间: {end_time}")