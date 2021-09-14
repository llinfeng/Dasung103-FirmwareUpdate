# About
This is an unofficial repo to circulate the firmware updates for Dasung 103
tablet. Dasung tech support does not mind circulating their firmware updates.

![approval text](approval_text.png)
Translate:
> Q: Do you guys mind me uploading the firmware to Github?
> A: We don't mind.

## Update (Version 3.0.14)
Change Log: 
```
【10.3英寸平板Not-eReader 103更新】3.0.14版本 （2021年9月10日） 
更新内容： 
1、增加了谷歌服务的开关（设置-应用和通知）        ==> Added "Google Play services" to the App info list under Settings/Apps&Notification
2、下拉栏增加了“位置”开关                       ==> Added a "Location" botton to the "Quick Panel" (swipe down from the top of the tablet for this panel)
3、多任务界面增加了内存使用情况                  ==> Added the current memory usage to the app-switcher view 
4、优化了APP安装界面                           ==> Udpated the installation confirmation box
5、优化了OTA流程，并增加了海内外服务器选择功能     ==> **Added an option to choose Mainland China as an option for the System upgrade server**
6、优化了低电量时自动关机的逻辑                  ==> When the battery is low, the device now shall turn off by itself.
7、修复了小语种下的定时休眠不匹配问题             ==> Fixed the auto-sleep timer for "other languages".
8、修复了一些你已知和你未知的bug……               ==> "Fixed some bug that you may or may not know about ...
【更新方式】平板的设置——系统——系统更新——检测更新（请提前连网并确认设备有足够电量的情况下再进行升级）
```

[**Click here**](https://www.dropbox.com/sh/3xlkgzsn9yb5kcb/AABr9EiVN5TGjOJ8YVTuUg5Aa?dl=0) to download all the necessary files for update 3.0.14. (This is a Dropbox link.) For detailed steps for updating the Dasung 103 tablet manually, please read along.

## Update (Version 3.0.13.210705)
Change Log:
* Fix the unexpected power-on issue when Bluetooth is kept active.
> Note, this cuts the overnight battery drain from 80% to 10% under sleep mode.

### How to update
Depending on your region, Dasung may or may not have pushed their firmware
updates to their server. If the auto-update works, great. If not, read along.
(Note, I have only tested the following procedures with Windowsd 10 machines. I
do not have a spare Dasung 103 tablet to test with macOS machines.)

### First, grab two zip files
It is costly to host files larger than 100MB on Github. Use [this Dropbox link](
https://www.dropbox.com/sh/gmrkazsnogspp6u/AACtYmCKp7hCS5MBVNmLKK8da?dl=0) to
download two zip-files for Version 3.0.13.210705. 
Through the Dropbox link, you can find the following:
* `platform-tools.zip` contains a `adb.exe` file, this is the workhorse shell that
  gets the job done.
* `update.zip` is the payload to be uploaded to the Dasung 103 tablet.


### Then, use `adb` to apply the firmware update
1. Unzip `platform-tools.zip` locally, and launch Command Prompt from the unzipped
   folder.
2. Move/Copy the `update.zip` file to the folder created in step 1. (Otherwise,
   the adb shell cannot find the payload directly.)
3. Connect the Dasung 103 tablet to the computer.
4. Navigate to the folder in step 1 using Command Prompt, and issue the
   following commands one by one
   ```
   adb push update.zip /data/ota_package/
   adb shell
   ```
   Then, carefully paste the following to the newly opened `adb shell`.
   ```
    update_engine_client --update --follow --payload=file:///data/ota_package/update.zip --offset=9034 --size=807766351 --headers="FILE_HASH=skZmkigtTTNayzPX7KG64Tbg7+YUairc25GI/96vCXU=
    FILE_SIZE=807766351
    METADATA_HASH=8fZx8Pn7JRBRbuo6Crp8+PBjfGklBgvlQ6Vx23hCp5o=
    METADATA_SIZE=108795
    "
   ```
   > Here is what to expect after issuing command `adb shell`:
   > ![adb shell, loaded](adb_shell_interface.png)

5. Wait for the update to finish (around 5-10 minutes)
6. Then, still in the `abd shell`, issue command: `reboot`. 
    (Note, through the abd shell, the `reboot` command is sent to the tablet
    and commands the tablet to restart.)
