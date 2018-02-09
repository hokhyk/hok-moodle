# Setting up your development environment for Moodle Mobile 2
## 1. install nvm
https://github.com/hokhyk/nvm
1. curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh | bash
2. export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
3. command -v nvm
## 2. install node (6.9.1)
nvm install 6.9.1
  nvm use 6.9.1

## 3. install cordova and ionic
npm cache clean
npm install -g cordova@6.5.0 ionic@2.2.3      # (If it throws an EACCESS error, run it again with sudo)
Please notice that Ionic 2.2.3 is being used. The CLI for Ionic 3 breaks our building system, there is an open issue to fix this: [http://tracker.moodle.org/browse/MOBILE-2112 MOBILE-2112].

## Install the npm required packages
sudo npm install -g bower                     # (This will install bower in a folder that should be in the PATH)
sudo npm install -g gulp                      # (This will install gulp in a folder that should be in the PATH)


# Clone the app base code
Clone the code base into a local directory in your computer.

git clone https://github.com/moodlehq/moodlemobile2.git moodlemobiledirectory
cd moodlemobiledirectory

# setup the npm packages
## 1. cd /home/vagrant/share/moodle/moodlemobile2
npm install  (This will install all the dependencies listed in package.json)

## 2. Add the iOS and Android platforms and install the required Cordova plugins
mkdir www
cordova prepare

Please, note that if you are creating a custom app with a custom URL scheme, you should edit the /config.xml file and specify there your custom URL_SCHEME (replacing the existing value) and your GCMPN SENDER_ID.

Run the following command to install the platforms and all the required Cordova plugins:

cordova prepare
Cordova Android 6.1.2 and Cordova iOS 4.3.1 have been verified to work fine with the app. If you're having problems with later versions you might want to check if it works with these versions.

## 3. Install javascript libraries (for moodlemobile2, this is not useful.)
bower install (this will install all the libraries listed in bower.json)

## 4. Run gulp’s default tasks (in order to create the build files)
gulp

## 5. Open the app in the browser
### start the Ionic server:
ionic serve --browser chromium

If you don't want to open any browser you should run:
ionic serve -b

# Updating ionic and cordova
sudo npm update -g cordova
sudo npm update -g ionic
Update project platforms:

ionic platform remove android
ionic platform remove ios
ionic platform add android
ionic platform add ios
Updating plugins
cordova plugin remove your_plugin_id
cordova plugin add your_plugin_id
Building for Android and iOS
Please see this guide to be able to build for Android and iOS using the command line:

http://cordova.apache.org/docs/en/5.0.0/guide_platforms_index.md.html#Platform%20Guides
