## [🔑](https://keys.openpgp.org/vks/v1/by-fingerprint/E616FA7221A1613E5B99206297966C06BB06757B) [Plebnet Playground ](http://github.com/PLEBNET-PLAYGROUND)
## [![plebnet-playground](https://github.com/PLEBNET-PLAYGROUND/plebnet-playground-docker/actions/workflows/plebnet-playground.yml/badge.svg)](https://github.com/PLEBNET-PLAYGROUND/plebnet-playground-docker/actions/workflows/plebnet-playground.yml)



```shell
git clone https://github.com/PLEBNET-PLAYGROUND/plebnet-playground-docker --config core.autocrlf=input && \
cd plebnet-playground-docker && \
pip3 install virtualenv  && \
python3 -m venv venv && \
source venv/bin/activate && \
pip3 install -r requirements.txt
```


<details>
<summary>👀</summary>
<p>

```shell
seq 0 947 | (while read -r n; do bitcoin-cli gettxout \
54e48e5f5c656b26c3bca14a8c95aa583d07ebe84dde3b7dd4a78f4e4186e713 $n \
| jq -r '.scriptPubKey.asm' | awk '{ print $2 $3 $4 }'; done) | \
tr -d '\n' | cut -c 17-368600 | xxd -r -p > bitcoin.pdf
```

</p>
</details>

<details>
<summary>👀</summary>
<p>

#### Referal Links:

[![DigitalOcean Referral Badge](https://web-platforms.sfo2.digitaloceanspaces.com/WWW/Badge%202.svg)](https://www.digitalocean.com/?refcode=ae5c7d05da91&utm_campaign=Referral_Invite&utm_medium=Referral_Program&utm_source=badge)

</p>
</details>