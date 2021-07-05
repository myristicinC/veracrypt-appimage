# veracrypt-appimage

These steps are adapted from: https://github.com/veracrypt/VeraCrypt/issues/501#issuecomment-554319569


- # 1. First, we need to make a directory called the AppDir (here we call it 'veracrypt.AppDir')  : 

cd ~/Documents
mkdir -p veracrypt/veracrypt.AppDir


- # 2. Then, we have to download the generic '.tar.bz2' linux Veracrypt installer : 

wget -c https://launchpad.net/veracrypt/trunk/1.24-update7/+download/veracrypt-1.24-Update7-setup.tar.bz2
mkdir -p veracrypt_archive/
tar -xf veracrypt-1.24-Update7-setup.tar.bz2 -C veracrypt_archive/
cd veracrypt_archive


- # 3. Then we have to : 
#- launch the installer 
#- accept the license, 
#- select extract 
#- and go to '/tmp' folder in order to extract the 'tar.gz' content into 'veracrypt.AppDir' : 

./veracrypt-1.24-Update7-setup-gui-x64 
cd /tmp
tar -xf veracrypt_1.24-Update7_amd64.tar.gz -C ~/Documents/veracrypt/veracrypt.AppDir/


- # 4. Copy the '/usr/share/applications/veracrypt.desktop' file into 'veracrypt.AppDir' : 
cd ~/Documents/veracrypt/veracrypt.AppDir/
cp ./usr/share/pixmaps/veracrypt.xpm .
cp ./usr/share/applications/veracrypt.desktop .


- # 5. Edit the veracrypt.desktop file as below to avoid any error message : 
nano veracrypt.desktop 

# veracrypt.desktop content shall be :
[Desktop Entry]
Encoding=UTF-8
Version=1.0
Name=VeraCrypt
GenericName=VeraCrypt
Comment=VeraCrypt
Exec=veracrypt
Icon=veracrypt
Terminal=false
Type=Application
Categories=Utility;


- # 6. Make the AppRun executable (and rename 'AppRun-x86_64' into 'AppRun' otherwise an error message happens) : 

wget -c https://github.com/AppImage/AppImageKit/releases/download/13/AppRun-x86_64
mv AppRun-x86_64 AppRun
chmod a+x AppRun


- # 7. Finally, we can package the whole 'veracrypt.AppDir' folder as an AppImage : 

cd ..
wget -c https://github.com/AppImage/AppImageKit/releases/download/13/appimagetool-x86_64.AppImage
chmod a+x appimagetool-x86_64.AppImage
./appimagetool-x86_64.AppImage veracrypt.AppDir ./Veracrypt-x86_64.AppImage


You can find your Veracrypt-x86_64.AppImage under ~/Documents/veracrypt/, already executable. You just need to double click or if you want from a terminal, launch ./Veracrypt-x86_64.AppImage under ~/Documents/veracrypt/.
