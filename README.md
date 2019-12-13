# Oracle CA Wallet Creator

Bash script to create a Oracle SSL Wallet containing all valid public root CA certificates.

Especially useful for dev environments or environments which interact with a lot of public web services or send emails via public providers.

The script uses CA certificates data from [Mozilla CA Certificate Store](https://www.mozilla.org/en-US/about/governance/policies/security-group/certs/), which is used by Firefox for example.


## Installation

```
git clone https://github.com/Dani3lSun/oracle-ca-wallet-creator.git
```

*Or just download the script here from GitHub*


## Usage

```
cd /path/to/oracle-ca-wallet-creator
. create_ca_wallet.sh
```

*After running the script, you will see an folder "wallet" which contains a Oracle Wallet file + a _pwd.txt file holding password information.*

Now you are ready to go, and you can deploy the wallet to any Oracle DB host. If you like to use this wallet for example with Oracle APEX, you can set the wallet as an instance wide default wallet:

```
begin
  apex_instance_admin.set_parameter('WALLET_PATH'
                                   ,'file:/path/to/wallet');
  apex_instance_admin.set_parameter('WALLET_PWD'
                                   ,'<pwd-from-pwd-file>');
  commit;
end;
/
```

*You can achieve the same by entering the wallet information in INTERNAL workspace of APEX: Manage Instance > Instance Settings > Wallet*

You can now use any public web service, mail provider or other SSL protected resource without dealing to create an wallet for each of them or add an extra certificate to an existing wallet.

See:

 - APEX_WEB_SERVICE package
 - APEX_MAIL package

for example...