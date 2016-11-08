## 証明書形式変換

### cert.pemファイルが作成
<pre>
openssl pkcs12 -clcerts -nokeys -out cert.pem -in cert.p12
</pre> 
パスワード入力して、下記のように出力されればOK.  
Enter Import Password:  
MAC verified OK  
### key.pemファイルが作成
<pre>
openssl pkcs12 -nocerts -out key.pem -in key.p12
</pre> 
パスワード入力して、下記のように出力されればOK.  
Enter Import Password:  
MAC verified OK  
Enter PEM pass phrase:  
Verifying - Enter PEM pass phrase:  
h3. key.pemからkey.unencrypted.pem作成  
<pre>
openssl rsa -in key.pem -out key.unecrypted.pem
</pre>
パスワード入力して、下記のように出力されればOK.  
Enter pass phrase for key.em:  
writing RSA key  
h3. 最後にapns.pemを生成  
<pre>
cat cert.pem key.unecrypted.pem > apns.pem
</pre>
下記のようにファイルが生成されたらOK.  
* cert.p12  
* key.p12  
* cert.pem  
* key.pem  
* key.unencryped.pem  
* apns.pem  

### サーバーにはapns.pemを送る