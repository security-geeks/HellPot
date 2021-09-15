# HellPot   
[![GoDoc](https://godoc.org/github.com/yunginnanet/HellPot?status.svg)](https://godoc.org/github.com/yunginnanet/HellPot) [![Go Report Card](https://goreportcard.com/badge/github.com/yunginnanet/HellPot)](https://goreportcard.com/report/github.com/yunginnanet/HellPot)


**CURRENTLY BROKEN FOR VERSIONS OF GO OVER 1.16.5**

**SEE THIS ISSUE:**  https://github.com/yunginnanet/HellPot/issues/2
  
**For the time being if you just plan on running HellPot, consider [downloading a release](https://github.com/yunginnanet/HellPot/releases).**
  
---  
  
HellPot is an endless honeypot that sends bots to hell. Based on [Heffalump](https://github.com/carlmjohnson/heffalump).   
  
  It finishes the work of Heffalump with a few improvements and the addition of a [toml configuration file](https://github.com/spf13/viper) and [JSON logging](https://github.com/rs/zerolog). It is built off of [CokePlate](https://git.tcp.direct/kayos/CokePlate).
    

The source of the honeypot data is [The Birth of Tragedy (Hellenism and Pessimism)](https://www.gutenberg.org/files/51356/51356-h/51356-h.htm) by Friedrich Nietzsche

![Exploding Heffalump](hellgif.gif)

Live example: <a href="https://vx-underground.org/wp-login.php" rel="nofollow">Do not follow this link.</a> It will flood your browser's memory and likely cause a crash.

## Example Web Server Config (nginx)  
    
```          
location '/robots.txt' {
	proxy_set_header Host $host;
	proxy_set_header X-Real-IP $remote_addr;
	proxy_pass http://127.0.0.1:8080$request_uri;
}  

location '/wp-login.php' {
	proxy_set_header Host $host;
	proxy_set_header X-Real-IP $remote_addr;
	proxy_pass http://127.0.0.1:8080$request_uri;
}
```


## Example Program Config (toml) 
  
  If the configuration  file is missing, the default settings will automatically drop itself in the current working directory as `config.toml`.  
    
```  
title = "HellPot"

[logger]
debug = false
log_directory = "./logs/"

[http]
bind_addr = "127.0.0.1"
bind_port = "8080"
# paths to be added to robots.txt that we will respond to
paths = [
        "wp-login.php",
        "wp-login",
]
```
  
