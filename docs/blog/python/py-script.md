# PyScript

[Official site](https://pyscript.net/)

[Github](https://github.com/pyscript/pyscript)

***Made by the people at [Anaconda](https://www.anaconda.com/)***

Finally, the framework that I've been waiting for! I've always loved Python but when it comes to the web, Python is mainly used as a backend language. Since I'm more of a designer, doing frontend work is the logical option.  

This new framework, which is still in its early stages, uses WebAssebly which is a powerful language to make the web feel like a native application.  The possibilities this opens up are encouraging and I think this will truly become even bigger in the next few years.  No doubt, JavaScript will still be around for a while but Python is a better language in my opinion. 

## Simple PyScript

This code snippets prints out the value for pi

```html
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- PYSCRIPT -->
  <link rel="stylesheet" href="https://pyscript.net/alpha/pyscript.css" />
  <script defer src="https://pyscript.net/alpha/pyscript.js"></script>

</head>
<body class="bg-black text-white grid place-items-center h-screen">
    <div>
    <py-script> print('This is Python in the browser') </py-script>
    <py-script>
print("Let's compute π:")
def compute_pi(n):
    pi = 2
    for i in range(1,n):
        pi *= 4 * i ** 2 / (4 * i ** 2 - 1)
    return pi

pi = compute_pi(100000)
s = f"π is approximately {pi:.3f}"
print(s)
    </py-script>
    </div>
    
</body>
</html>
```