# How to Add Cookie in DotDotPwn

Video tutorial

[![Watch the video](https://img.youtube.com/vi/83wNHL6K5z0/maxresdefault.jpg)](https://youtu.be/83wNHL6K5z0)

## Prerequisites

- Have downloaded DotDotPwn
- Have downloaded cURL

## How to run this Spring Boot App

Please check the dependencies on `pom.xml` and 
the if you have all dependencies, then run

```bash
mvn install
java -jar target\demo-0.0.1-SNAPSHOT.jar (windows)
```

Open `localhost:8081/testing` to see one of the endpoints.

Default username and password are `user`

## How to see all fuzzes in DotDotPwn

Type this 

```bash
for fuzz_pattern in $(./dotdotpwn.pl -m stdout -d 2); do echo $fuzz_pattern; done
```

## cURL command without Cookie

```shell
curl -I -X GET "http://<wifi_private_ip_address>:8081/testing" \
    -H "Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7"
```

## cURL command with Cookie

```shell
curl -I -X GET --location "http://<wifi_private_ip_address>:8081/testing" \
    -H "Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7" \
    -H "Cookie: JSESSIONID=<the_cookie>"
```

## The command to combine cURL with DotDotPwn

```shell
rm output.txt
for fuzz_pattern in $(./dotdotpwn.pl -m stdout -d 2); do
    echo "---------- SEPARATOR ----------" >> output.txt 
    curl -X GET --location "http://<wifi_private_ip_address>:8081/testing/$fuzz_pattern" \
    -H "Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7" \
    -H "Cookie: JSESSIONID=<the_cookie>" >> output.txt; done
```

## Note

The Docker Container in this video

https://hub.docker.com/r/hackersploit/bugbountytoolkit
