# 🧪 PIRLTest Project
This project contains 2 sides - framework and device sides.

The framework side implements the core method of PIRLTest, while the device side implements the interaction with devices and the whole process of PIRLTest.

## 🖥️ The Framework Side
The framework side implements an HTTP server for the device side.

⚠️ A Linux server with GPU and CUDA support is necessary for deployment.

### 🚀 Deployment
1. 📦 Install the requirements.
```sh
pip install -r requirements.txt
```
2. ⚙️ Config OCR. Modify the `ocr()` method in `img_process/ocr_canny.py` (use your own id and keys).
3. ▶️ Run the app.
```sh
./run.sh
```

✅ It is deployed on http://localhost:5000.


## 📱 The Device Side
The device side is an application. It can run on a server connected to Android devices for Android testing, or on a computer with Chrome installed for Web testing.

🔐 We use SSH as the protocol to connect server where the framework side deploys. So make sure that SSH service is running on your server.

### 📋 Preparation
1. 📦 Install the requirements.
```sh
pip install -r requirements.txt
```
2. 🔐 Config SSH: modify `configs/ssh_config.json`. Specify ip, port, username and password.
3. 📝 Test config: create a test config file under `configs` folder. 
3. 💡 Take `configs/android/wikipedia.json` and `configs/web/webogram.json`as examples. 
	- `platform`: `android` or `web`
	- `serial_no`: the serial number of the **Android** device
	- `screen_size`: the screen size of the device
	- `pre_interact`: whether to manually log in the app before testing
	- `server_proj_dir`: the path of where the framework side deploys
	- `server_screenshot_dir`: `screenshots` only
	- `local_screenshot_path`: where the screenshot saves locally
	- `window_keys`: not used
	- `total_time`: testing time in seconds
	- `banner_height`: The height of the top status bar of **Android** device.
	- `remote_port`: the port of the framework side
	- `app.name`: the name of the app under test
	- `app.pkg`: the package of the **Android** app
	- `app.main_activity`: the main activity of the **Android** app
	- `app.url`: the url of the **Web** app
4. 🌐 Update chromedriver.exe if testing web application.

### ▶️ Run
For Android app testing, use the following command:
```sh
python pirltest_android.py <config_path>
```

For Web app testing, use the following command:
```sh
python launcher.py <config_path>
```

### 📊 After Testing
For Android apps, if instrumented properly, the .exec coverage data files would be pulled to `coverages` folder. For Web apps, if instrumented properly, the .json coverage data file would be downloaded under `$HOME/Download` folder.

📄 The log of the device side would be under `logs` folder.

📸 All the screenshots and the framework side logs would be on the server.
