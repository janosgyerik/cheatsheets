```
# urlencode
echo some_url | perl -MURI::Escape -ne 'chop; print uri_escape($_), "\n"'

# base64 encode
perl -MMIME::Base64 -e '$a = join("", <>); print encode_base64($a)' < input

# base64 decode
perl -MMIME::Base64 -e '$a = join("", <>); print decode_base64($a)' < input
```
