
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
`gobuster dir -u https://3b71fd43f1fb10e3401857b7bf59ed00.ctf.hacker101.com/  -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -o petshop.txt`

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


