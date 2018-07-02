## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/Snake002/proyecto/edit/master/README.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/Snake002/proyecto/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.

Juego "snake"

# -*- coding: utf-8 -*- 
 
import os 
import random 
import pygame 
from pygame.locals import * 
 
pygame.display.init() 
window = pygame.display.set_mode((300, 300)) 
clear = window.copy() 
sizepoint = 10 
dir = 1 
snake = [(15, 15)] 
apple = [(5, 5)] 
main_clock = pygame.time.Clock() 
while True: 
    for eventos in pygame.event.get(): 
        if eventos.type == QUIT: 
            pygame.quit() 
            os.sys.exit(0) 
        elif eventos.type == KEYDOWN: 
            print(eventos.key) 
            if eventos.key == 273: 
                dir = 1 
            elif eventos.key == 274: 
                dir = 2 
            elif eventos.key == 275: 
                dir = 3 
            elif eventos.key == 276: 
                dir = 4        
    window.blit(clear, (0, 0))         
    for node in snake: 
        x, y = node 
        pygame.draw.rect(window, (255, 255, 255), ((x * sizepoint, y * sizepoint), (sizepoint, sizepoint)), 1) 
    x, y = apple[0]     
    pygame.draw.rect(window, (255, 0, 0), ((x * sizepoint, y * sizepoint), (sizepoint, sizepoint)), 1) 
    if dir == 1: 
        x, y = snake[0] 
        y -= 1 
        y = 29 if y < 0 else y 
        snake.insert(0, (x, y)) 
    elif dir == 2: 
        x, y = snake[0] 
        y += 1 
        y = 0 if y > 29 else y 
        snake.insert(0, (x, y)) 
    elif dir == 3: 
        x, y = snake[0] 
        x += 1 
        x = 0 if x > 29 else x 
        snake.insert(0, (x, y)) 
    elif dir == 4: 
        x, y = snake[0] 
        x -= 1 
        x = 29 if x < 0 else x 
        snake.insert(0, (x, y)) 
    if snake[0] in snake[1:]: 
        print("Has perdido") 
        pygame.quit() 
        os.sys.exit(0) 
    if not snake[0] in apple: 
        snake.pop(len(snake) - 1) 
    else: 
        apple.pop(0) 
        apple.append((random.randint(0, 29), (random.randint(0, 29))))   
    main_clock.tick(10) 
    pygame.display.flip()

