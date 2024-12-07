---
layout: default
---

# SDL Renderer

<img src="SDLRender.png" alt="SDL Renderer">
Test texture being rendered into an SDL window.

## Goal
This project is still in early development, but I thought it was worth mentioning future projects. This project is a C++ renderer using the SDL library. Currently the basics are still necessary abstractions such as sprites, math functions and input (keyboard and mouse). Past this point I want to create a 2D rage platformer video game. This project is mainly for learning graphics, less so for game design, therefore I don't expect to make a expansive game. A real priority for this is optimizations, I wrote this project in C++ rather than a game engine mostly because of the performance benefit. This is because C# (which is used by game engines) and other alternatives aren't compiled to machine code but to an intermidiate language (C# IL or Java Bytecodes). This makes them much slower and restricts control over the hardware than native C++.

## Example Code
```cpp
void Renderer::render() {

    //background color
    SDL_SetRenderDrawColor(this->m_renderer, 255, 0, 0, 255);
    SDL_RenderClear(this->m_renderer);

    int* mouseX = new int();
    int* mouseY = new int();
    SDL_GetMouseState(mouseX, mouseY);

    SDL_Rect rect = rectCentered(*mouseX, *mouseY, 50, 50);

    //rect color
    SDL_SetRenderDrawColor(this->m_renderer, 0, 255, 0, 255);

    // Render rect
    SDL_RenderFillRect(this->m_renderer, &rect);

    renderCenteredSprite(testSprite, *mouseX, *mouseY);

    delete mouseX;
    delete mouseY;

    //SDL_UpdateWindowSurface(m_window);



    // Render frame to the screen DON'T CALL THIS MORE THAN ONCE PER FRAME
    SDL_RenderPresent(this->m_renderer);
}

```
Main render method.