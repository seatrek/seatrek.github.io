
## Update AMP caches

```bash
echo -n >url.txt "/update-cache/c/s/seatrek.github.io/1?amp_action=flush&amp_ts=$(date +%s)" && cat url.txt | openssl dgst -sha256 -sign private-key.pem >signature.bin
echo -n '&amp_url_signature=' >>url.txt
cat signature.bin | base64 --wrap=0 | sed 's/+/-/g; s/\//_/g' >>url.txt
cat url.txt

curl "https://seatrek-github-io.cdn.ampproject.org$(cat url.txt)"
curl "https://seatrek-github-io.amp.cloudflare.com$(cat url.txt)"
curl "https://seatrek-github-io.bing-amp.com$(cat url.txt)"
curl "https://cdn.ampproject.org/caches.json"
```