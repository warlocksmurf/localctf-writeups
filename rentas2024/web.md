# Credits
@Shen completed all web challenges and even first blooded one of them, so credits for him on the web category writeup.

# Task 1: bring your own script
Question:

Flag: `RWSC{J4CKP0T}`

We are given a website that has multiple directories and the flag should be located in one of them. He made a script to brute force each path and found out the flag was actually an image.

```
import requests
from bs4 import BeautifulSoup
from urllib.parse import urljoin
from urllib.parse import unquote
visited_links = set()

## FLAG URL
## https://byos.ctf.rawsec.com/root/%F0%9F%A4%A4%F0%9F%A4%95%F0%9F%98%83/%F0%9F%98%94%F0%9F%98%81%F0%9F%98%95%F0%9F%98%B5/%F0%9F%98%BA%F0%9F%98%AA%F0%9F%A5%B4%F0%9F%98%87/%F0%9F%A5%B0%F0%9F%A5%B6%F0%9F%A4%A3%F0%9F%98%82/%F0%9F%A4%A7%F0%9F%98%85/index.php

def get_links(url):
    try:
        response = requests.get(url)
        soup = BeautifulSoup(response.text, 'html.parser')
        links = soup.find_all('a', href=True)
        return [urljoin(url, link['href']) for link in links]
    except requests.exceptions.RequestException as e:
        print(f"Error retrieving links from {url}: {e}")
        return []

def no_directories_found(soup):
    return "No directories found." not in soup.get_text() and not soup.find_all(class_="directory-link")

def visit_links_recursive(url):
    if url in visited_links:
        return

    print(f"Visiting: {unquote(url)}")

    try:
        response = requests.get(url)
        soup = BeautifulSoup(response.text, 'html.parser')

        if no_directories_found(soup):
            print(f"Flag on: {url}")
            exit()

        visited_links.add(url)

        links = get_links(url)

        for link in links:
            visit_links_recursive(link)

    except requests.exceptions.RequestException as e:
        print(f"Error visiting {url}: {e}")

def main():
    starting_url = 'https://byos.ctf.rawsec.com/root/'
    visit_links_recursive(starting_url)

if __name__ == "__main__":
    main()

```

```
...
Visiting: https://byos.ctf.rawsec.com/root/🤤🤕😃/😌/🥺😄/🤒🤯🤕/index.php
Visiting: https://byos.ctf.rawsec.com/root/🤤🤕😃/😌/🥺😄/🤒🤯🤕/😏/index.php
Visiting: https://byos.ctf.rawsec.com/root/🤤🤕😃/😔😁😕😵/index.php
Visiting: https://byos.ctf.rawsec.com/root/🤤🤕😃/😔😁😕😵/😺😪🥴😇/index.php
Visiting: https://byos.ctf.rawsec.com/root/🤤🤕😃/😔😁😕😵/😺😪🥴😇/😳🤕/index.php
Visiting: https://byos.ctf.rawsec.com/root/🤤🤕😃/😔😁😕😵/😺😪🥴😇/😳🤕/👾/index.php
Visiting: https://byos.ctf.rawsec.com/root/🤤🤕😃/😔😁😕😵/😺😪🥴😇/🥰🥶🤣😂/index.php
Visiting: https://byos.ctf.rawsec.com/root/🤤🤕😃/😔😁😕😵/😺😪🥴😇/🥰🥶🤣😂/😅/index.php
Visiting: https://byos.ctf.rawsec.com/root/🤤🤕😃/😔😁😕😵/😺😪🥴😇/🥰🥶🤣😂/😅😡/index.php
Visiting: https://byos.ctf.rawsec.com/root/🤤🤕😃/😔😁😕😵/😺😪🥴😇/🥰🥶🤣😂/🤧😅/index.php
Flag on: https://byos.ctf.rawsec.com/root/%F0%9F%A4%A4%F0%9F%A4%95%F0%9F%98%83/%F0%9F%98%94%F0%9F%98%81%F0%9F%98%95%F0%9F%98%B5/%F0%9F%98%BA%F0%9F%98%AA%F0%9F%A5%B4%F0%9F%98%87/%F0%9F%A5%B0%F0%9F%A5%B6%F0%9F%A4%A3%F0%9F%98%82/%F0%9F%A4%A7%F0%9F%98%85/index.php
```

![image](https://github.com/warlocksmurf/localctf-writeups/assets/121353711/efc696a8-7f06-4431-a017-e89fe3197486)

# Task 2: 
Question:

Flag: `RWSC{}`

We are given a website that has multiple directories and the flag should be located in one of them. He made a script to brute force each path and found out the flag was actually an image.
