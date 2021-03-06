# PrivateBlog
Private blog agregator for emercoin blockchain

This is a blog aggregator. All posts are stored in emercoin blockchain. The posts can be either anonymous or have anonymous blogger as an author. The posts can also reply to each other. The posts can be created, updated or deleted only by an owner of emercoin wallet using name-value storage (NVS).

The blockchain values from NVS gets parsed by this aggregator using @key="value" params inside the NVS value.

YouTube chanel https://www.youtube.com/channel/UC_iKEMc1lkxeMus2yArktLQ !!!

Installer https://github.com/tolik-punkoff/privateblog-installer and https://mega.nz/#!sJcnWCaa!fKG5DRC8cehMhitpeerb-TrbaQGA_oP1cUd-z3tKjFo by tolik-punkoff

## Install
### Linux
`bash build_and_install_linux.sh` to install to any linux
And go to `/home/{your-username}/pblog` and run `./run.sh`
### Windows
* Download PHP from `https://windows.php.net/download/` and unzip it to `C:\php`
* Make sure that `C:\php` is in *Path* enviroment variable
* Instal MS Visual Studio Redistributable (found here `https://support.microsoft.com/en-us/help/2977003/the-latest-supported-visual-c-downloads`)
* Run `build_and_install_windows.bat` and then run `run-private-blog.bat` from your desktop (the `build_and_install_windows.bat` will also copy and overwrite `C:\php\php.ini` with a new one)
### Manual (or other OS)
* Make shure that *sqlite3* *mbstring* *xmlrpc* *curl* extensions is on and *shorttags* (<?) is on in *php.ini*
* Run `php compile.php` to build `pblog.phar` and copy it to `build` directory
* Then go to `build\install\other` and execute
    `php config.php -f="{EMERCOIN}/emercoin.conf"` this will grab configuration from `emercoin.conf` to `config.json` file where {EMERCOIN} is emercoin wallet directory with emercoin.conf, wallet.dat and blockchain DB
* Run `php -S localhost:8000 pblog.phar` to start a server

## Run
* Run browser with address `http://localhost:8000`
* Make sure your Emercoin wallet is running and unlocked

## Build
Build Phar using `php compile.php`
And configure `conf/conf.php` and set
```
define('PHAR', true);
define('SQLITE', true);
```
before compiling

## Do bloging through web interface
Finally added ability to make records not through Emercoin wallet, but through Private Blog WEB interface

Added editor and display of multiple replies

## Register a blogger (optional)
1. Create a record named blogger:username in emercoin NVS
2. Add optional value as a user description. 

* @key emercoin address (example ENwm9Aq8vHgTW6akyti3vQSZJK2qPAGaYW)
* @sig the bloggers signature, result of signmessage "emercoinaddress" "username" command from emercoin console or RPC

## Make a post
1. Create a record named blog:postname in emercoin NVS
2. The value will be the post body.
* The body can contain all HTML tags except < script > tag 

* @title title of a post (optional)
* @lang the ISO_639-1 code of post language (optional, default en)
* @username username of blogger (optional)
* @sig (optional used with @username) 
The result of signmessage "emercoinaddress" "username:postname" command, where emercoinaddress is @key from user's record and postname is this post name from blog:postname. This signature gets verified by verifymessage "emercoinaddress" "@sig" "username:postname" command
* @keywords "drugs,sex,rockandroll" (optional)
* @reply the name of the post you want to reply to (optional)

## Make a reply to other post
* Any post can reply to any other post using @reply keyword 
* @reply the name of the post you want to reply to

## @ Symbol
* @@

## Links to other posts
 #post_name_link_to="link caption"

## Post, that includes other posts or post > 20kb
Inside post: %%subpost_name%%
Max level of subposts is 5

## Big files
 Large files > 20kb is divided into parts

 Execute console commands:
1. split --bytes=18k Konrad_Curze_sketch_small.jpg
2. md5sum Konrad_Curze_sketch_small.jpg
3. file -b --mime-type Konrad_Curze_sketch_small.jpg
 
 Create NVS records

* file:file_hash (file:3d9c09df0d72f0a3b02d03a89d2ee5b1)
* {"content_type": "image/jpeg", "name": "Konrad_Curze_sketch_small.jpg", "parts": 5}

* file:file_hash:1 (file:3d9c09df0d72f0a3b02d03a89d2ee5b1:1) - part 1 of file Konrad_Curze_sketch_small.jpg
 ...
* file:file_hash:5 - part 5
 

 $$$hash_of_file - url to file
 $hash_of_file="link caption" - link to file

## Links
* Emercoin http://emercoin.com/
* Market cap http://coinmarketcap.com/currencies/emercoin/#markets

## Uses

###### MeekroDB http://meekro.com/
###### Bootstrap http://getbootstrap.com/
###### Parsedown mardown parser https://parsedown.org/
###### SimpleMDE Markdown editor https://simplemde.com/

## Donate

###### Emercoin EQkpLeX4FhqxnoXdPMJqnaHxJHHgNgTKLh
###### Bitcoin 1JU7QyyiavuKeZvCkxA269a3wnf8qb1S5p