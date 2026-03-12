# WebC

An ambitious C library to do full-stack web development without the usual nonsense of the field.

## Key Features (more like todo list)

- Raylib like simple API
- Folder-based routing (can be configured away from this)
- Simple reactivity
- Seamless integration with existing libraries (at ABI level)
- GPU rendering by default
- WebAsm centric

## Example Program (vision)

### Basic Webpage

```c
#define WEBC_IMPL
#include <webc.h>

#define PORT 8888

void button() { Notice("You pressed a button!"); }

void main()
{
    WebEngineInit(PORT);

    WebRenderBegin();
        Heading("Hello, World", DEFAULT_STYLE);
        Button("I am a button", button);
    WebRenderEnd();
}
```

### Less Skeletal Webpage

```c
#define WEBC_IMPL
#define GPU_RENDER
#define MAX_MEMORY_POOL 1024
#include <webc.h>

#define PORT 8888

void main()
{
    WebEngineInit(PORT);
    RenderMode(DEFERRED | AUTO_SSR);
    EnableAutoHotReload(ON_SAVE);

    WebRenderBegin();

        SetLayoutBodyColour(WEB_BLACK);
        SetLayoutTextColour("#ff3324");

        AddToLayout(Navbar("navbar_main", ATTACH_TOP | FIXED, 100, WIDTH_FULL));
        SetComponentStyle("navbar_main", "text-lg text-color-black")

        LayoutMode(LEFT_RIGHT_STACK, "navbar_main");
            Logo("assets/logo.svg", AUTO_STYLE);
            Heading("Example Website", AUTO_STYLE);
            Flex();
            SearchBar(search, AUTO_STYLE);
            ButtonTransparent("About", "text-white", Route("/about"));
            ButtonIconDefine("<svg: ...>", Route("https://github.com/user/project"));
            ButtonThemeSwitchIcon("assets/day.svg", "assets/night.svg", ComputeNightTheme(), NULL);

        LayoutMode(TOP_DOWN_COLUMN, "body");
            Heading("Example Heading", "text-xl");
            Paragraph("Lorem Ipsum .............. Some interesting text");
            Id(ButtonSolid(
                Text("Call To Action", ModifyStyle(UNDERLINE_DOTTED, GAP, 0.2f)) createSecret),  "btn_call");
            ButtonOutline(Text("Learn More", CopyStyleById("btn_call")), learnMore);

            Reactive(Id(Span("1"), "counter_span"));
            ReactiveButton("+", "counter_span", addToCounter);

        LayoutMode(LEFT_RIGHT_STACK, "body");
            Image("assets/img1.png");
            ImageLink("assets/img2.png", Route("/share"));
            Image("assets/img3.png");
        
        LayoutModeEnd();
    WebRenderEnd();
}
```

## Contribution

Feel free to contribute in any way. Raise issues or send PRs.

## License

The library is licensed under GNU GPL-2.0 except modules which have their separate license.
