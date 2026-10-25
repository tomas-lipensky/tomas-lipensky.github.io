# Node-Red

### Externi odkazy

[Seznam prikazu a objektu](http://ss64.com/vb/)  
[Scriptovani na MS](http://technet.microsoft.com/en-us/library/ee198844.aspx)  

### Instalace offline (na intranetu)

npm install -g npmbox ... instalace nmpbox balicku  
npmbox npmbox ... stahne npmbox a zavislosti do balicku  
npm install pm2 -g ... nainstaluje se libovolny balik, treba pm2  
npmbox pm2 ... zabali se nainstalovany balik  
scp npmbox.npmbox pm2.npmbox root@offline-server:. ... pretahne se balicek npmbox.npmbox a pm2 na vzdaleny offline server  
ssh  root@offline-server ... pripojime se na server  
tar --no-same-owner --no-same-permissions -xvzf npmbox.npmbox ... rozbali se archiv  
npm install --global --cache ./.npmbox.cache --optional --cache-min 99999999999 --shrinkwrap false npmbox ... nainstaluje se obsah balicku - npmbox  
npmunbox pm2.npmbox --global ... nainstaluje se pm2 z baliku  

##### Jiny zpusob

npm cache clear  
npm install -g **package.x.y.z**  
scp -R /.npm/* **/cache-whatever-folder**  
npm cache clear  
npm install --global --cache **/cache-whatever-folder** --optional --cache-min 99999999999 --shrinkwrap false **package.x.y.z**  

[offline-npm](https://www.npmjs.com/package/offline-npm) ... dalsi alternativa  

### nastaveni, bezpecnost

[node-red](https://gist.github.com/DaveThw/da394c8d04fa2bba55ac) ... skript na systemd (systemctl) sluzbu  
/usr/local/lib/node_modules/node-red/settings.js ... globalni nastaveni  
~/.node-red/settings.js ... lokalni nastaveni  
cd /usr/local/lib/node_modules; node -e "console.log(require('bcryptjs').hashSync(process.argv[1], 8));" "aaa" ... vygeneruje heslo  
openssl genrsa -out privkey.pem  
openssl req -new -x509 -key privkey.pem -out cert.pem -days 1095  
[Nastaveni https, ldap, ...](http://www.hardill.me.uk/wordpress/2015/05/11/securing-node-red/)  
[Reverse proxy](https://openenergymonitor.org/forum-archive/node/12489.html) pro Node-Red  

### Administrace

[How to backup flows and related configuration](https://github.com/node-red/cookbook.nodered.org/wiki/How-to-backup-flows-and-related-configuration) ... backup a restore Nodered  

### Promenne

context.get('count') ... nacte promennou count (lokalni v nodu)  
flow.set('count', hodnota) ... zapise do promenne count hodnotu promenne hodnota (lokalni v celem flow)  
global.get('count') ... nacte globalni promennou count  
return {payload : msg.payload.a.b[1].cislo } vrati hodnotu nactenou ze vstupu (msg.payload) a protoze to je objekt, referuji na konkretni vlastnost objektu  

====Email====

```
msg = {
 payload : "Obsah mailu" + Date().toString(),
 topic : "Subject",
 to : "1@a.b, 2@a.b",
 cc : "3@a.b"
 bcc : "4	@a.b"
};
return m sg
```

### bloky (flows)

[forEach (array iteration & completion)](https://flows.nodered.org/flow/43501a1b424434de0ffb)  
[node-red-contrib-actionflows](https://flows.nodered.org/node/node-red-contrib-actionflows)  
[GPIOd](https://flows.nodered.org/node/node-red-node-pi-gpiod) - ovladani GPIO sbernice na Raspberry  

### Priklady

##### Webove stranky

[Node-red web page – an example to get you started](http://l0l.org.uk/2014/01/simple-node-red-web-page/) - jednoduche webove stranky s daty z casovace  
[Work with cookies](https://cookbook.nodered.org/http/work-with-cookies) - ukazka prace s cookies]]
[[http://developers.sensetecnic.com/article/sentiment-chat-with-node-red/|How to Build a Great Chat Application With Node-RED and Websockets  
[A Node-RED web user interface builder](https://github.com/TotallyInformation/node-red-contrib-uibuilder) - vytvareni uzivatelskeho prostredi s NodeRed - priklad s JQuery, Riot, MoonJS, Umbrella JS  
##### MongoDB

[Workflow based visual programming with Node Red](https://medium.com/@motiooon/workflow-based-visual-programming-with-node-red-81b720359c7)Prace s MongoDB  
[Mongodb et Node-red](http://www.rgot.org/mongodb-et-node-red/) ... Videa od François Riotte  
#### Ostatni

[Node-RED Design Patterns](https://medium.com/node-red/node-red-design-patterns-893331422f42) ... popisy Node-Red konstrukci  
[Node-RED Forms and Templates](https://www.coursera.org/learn/developer-nodered/lecture/sxBvz/node-red-forms-and-templates)  
[Node-RED Dashboard Template Examples (AngularJS)](https://totallyinformation.github.io/nr-qa/dashboard-template-examples.html)  
[Authenticating Node-RED with JSONWebToken](https://www.compose.com/articles/authenticating-node-red-with-jsonwebtoken/) - popis i animovane obrazky  
[Authenticating Node-RED using JSONWebToken - Part 2](https://www.compose.com/articles/authenticating-node-red-using-jsonwebtoken-part-2/) - popis i animovane obrazky  
[5-minute Signup Forms with Node-RED and Compose](https://www.compose.com/articles/5-minute-signup-with-node-red-and-compose/) - popis i animovane obrazky  
[Power Prototyping with MongoDB and Node-RED](https://www.compose.com/articles/power-prototyping-with-mongodb-and-node-red-2/) - popis i animovane obrazky  
[Quick Connections for MongoDB with Node-RED](www.compose.com/articles/quick-connections-for-mongodb-with-node-red/) - popis i animovane obrazky  

]]
