# ybc Bulma docs example
This repo contains a quick run down of some functionality of the ybc crate library. The examples here try to use the various examples listed in the bulma documention as a template, following closely in order to arrive at the same end result in both look and style. Hopefully this allows for some sort of synergy between both docs. For now only Navbar functionality is explored. If deemed beneficial, the rest of the ybc library will be explored, resulting a simple website that hopefully may act as a useful reference.

## Example - Navbar

<p align="center">
    <img src="https://i.imgur.com/sALk87F.gif">
</p>

### Code
<details>
    <summary>Example</summary>

```rust
struct Model {
    // `ComponentLink` is like a reference to a component.
    // It can be used to send messages to the component
    link: ComponentLink<Self>,
    value: i64,
}

impl Component for Model {
    fn view(&self) -> Html {
        html! {
            // ybc-element of type Navbar. navbrand, navstart, and navend properties are required and each expect an Html type. The yew html! macro returns this type.
            // The `navbar-burger` section is automatically appended.
            <ybc::Navbar navbrand=self.view_navbrand() navstart=self.view_navstart() navend=self.view_navend() />
        }
    }
}

impl Model {
    // Contruct the contents of the Navbar brand section and return Html type that navbrand property of Navbar expects.
    // Html type gets tossed into navbrand field of NavbarProps struct. Consult ybc Docs for more info.
    fn view_navbrand(&self) -> Html {
        html! {
            <>
                <ybc::NavbarItem tag=A>
                    <img src="https://bulma.io/images/bulma-logo.png" />
                </ybc::NavbarItem>
            </>
        }
    }

    // Contruct Navbar navdrop Menu
    fn view_navdrop(&self) -> Html {
        html! {
            <ybc::NavbarDropdown navlink=self.view_navlink() hoverable=true>
                <ybc::NavbarItem tag=A>
                    { "About" }
                </ybc::NavbarItem>
                <ybc::NavbarItem tag=A>
                    { "Jobs" }
                </ybc::NavbarItem>
                <ybc::NavbarItem tag=A>
                    { "Contact" }
                </ybc::NavbarItem>
                <ybc::NavbarDivider />
                <ybc::NavbarItem tag=A>
                    { "Report an issue" }
                </ybc::NavbarItem>
            </ybc::NavbarDropdown>
        }
    }

    // Contruct the contents of the `navbar-end` section and return Html type that navend property of Navbar expects.
    // Html type gets tossed into navend field of NavbarProps struct. Consult ybc Docs for more info.
    fn view_navend(&self) -> Html {
        html! {
            <ybc::NavbarItem tag=Div>
                // Create div container for button groups
                <ybc::Buttons>
                    // Button classes property accepts Option<String> type. `is-primary` here provides color styling. 
                    <ybc::Button classes=Some("is-primary")>
                        <strong>{ "Sign up" }</strong>
                    </ybc::Button>
                    <ybc::Button classes=Some("is-light")>
                        { "Log in" }
                    </ybc::Button>
                </ybc::Buttons>
            </ybc::NavbarItem>
        }
    }

    // Contruct the contents of the `navbar-link` section and return Html type that navlink property of NavbarDropdown expects.
    // Html type gets tossed into navlink field of NavbarDropdownProps struct. Consult ybc Docs for more info.
    fn view_navlink(&self) -> Html {
        html! {
            { "More" }
        }
    }

    // Contruct the contents of the `navbar-start` section and return Html type that navstart property of Navbar expects.
    // Html type gets tossed into navstart field of NavbarProps struct. Consult ybc Docs for more info.
    fn view_navstart(&self) -> Html {
        html! {
            <>
                <ybc::NavbarItem tag=A>
                    { "Home" }
                </ybc::NavbarItem>
                <ybc::NavbarItem tag=A>
                    { "Documentation" }
                </ybc::NavbarItem>
                { self.view_navdrop() }
            </>
        }
    }
}
```
    
</details>

## Example - Main page body

<p align="center">
    <img src="https://i.imgur.com/fwgWLDw.gif">
</p>

### Code
<details>
    <summary>Example</summary>

```rust
struct Model {
    // `ComponentLink` is like a reference to a component.
    // It can be used to send messages to the component
    link: ComponentLink<Self>,
    value: i64,
}

impl Component for Model {
    fn view(&self) -> Html {
        html! {
            <>
                // ybc-element of type Navbar. navbrand, navstart, and navend properties are required and each expect an Html type. The yew html! macro returns this type.
                // The `navbar-burger` section is automatically appended.
                <ybc::Navbar navbrand=self.view_navbrand() navstart=self.view_navstart() navend=self.view_navend() />

                // ybc-element of type Tile. Is a container for all other tiles that compose the main body of webpage.
                <ybc::Tile ctx=Ancestor>
                    { self.view_main() }
                </ybc::Tile>
            </>
        }
    }
}

impl Model {
    // Construct contents of main section of webpage. 
    fn view_main(&self) -> Html {
        html! {
            <>
                // Tile element used to build grid layouts. 
                // Has optional properties children: Children, classes: Option<String>, tag: String, ctx(context modifier): Option<TileCtx>, vertical: bool, and size: Option<TileSize>
                <ybc::Tile vertical=true size=TileSize::Eight>
                    <ybc::Tile>
                        <ybc::Tile ctx=Parent vertical=true>
                            <ybc::Tile ctx=Child tag="article" classes=Some("notification is-primary")>
                                <p class="title">{ "Vertical..." }</p>
                                <p class="subtitle">{ "Top tile" }</p>
                            </ybc::Tile>
                            <ybc::Tile ctx=Child tag="article" classes=Some("notification is-warning")>
                                <p class="title">{ "...titles" }</p>
                                <p class="subtitle">{ "Bottom tile" }</p>
                            </ybc::Tile>
                        </ybc::Tile>
                        <ybc::Tile ctx=Parent>
                            <ybc::Tile ctx=Child tag="article" classes=Some("notification is-info")>
                                <p class="title">{ "Middle tile" }</p>
                                <p class="subtitle">{ "With an image" }</p>
                                <figure class="image is-4by3">
                                    <img src="https://bulma.io/images/placeholders/640x480.png" />
                                </figure>
                            </ybc::Tile>
                        </ybc::Tile>
                    </ybc::Tile>
                    <ybc::Tile ctx=Parent>
                        <ybc::Tile ctx=Child tag="article" classes=Some("notification is-danger")>
                            <p class="title">{ "Wide tile" }</p>
                            <p class="subtitle">{ "Aligned with the right tile" }</p>
                            <div class="content">
                                <p>{ "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin ornare magna eros, eu pellentesque tortor vestibulum ut. Maecenas non massa sem. Etiam finibus odio quis feugiat facilisis." }</p>
                            </div>
                        </ybc::Tile>
                    </ybc::Tile>
                </ybc::Tile>
                <ybc::Tile ctx=Parent>
                    <ybc::Tile ctx=Child tag="article" classes=Some("notification is-success")>
                        <div class="content">
                            <p class="title">{ "Tall title" }</p>
                            <p class="subtitle">{ "With even more content" }</p>
                            <div class="content">
                                <p>
                                    {
                                        "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Etiam semper diam at erat pulvinar, at pulvinar felis blandit. Vestibulum volutpat tellus diam, consequat gravida libero rhoncus ut. Morbi maximus, leo sit amet vehicula eleifend, nunc dui porta orci, quis semper odio felis ut quam."
                                    }
                                </p>
                                <p>
                                    {
                                        "Suspendisse varius ligula in molestie lacinia. Maecenas varius eget ligula a sagittis. Pellentesque interdum, nisl nec interdum maximus, augue diam porttitor lorem, et sollicitudin felis neque sit amet erat. Maecenas imperdiet felis nisi, fringilla luctus felis hendrerit sit amet. Aenean vitae gravida diam, finibus dignissim turpis. Sed eget varius ligula, at volutpat tortor."
                                    }
                                </p>
                            </div>
                        </div>
                    </ybc::Tile>
                </ybc::Tile>
            </>
        }
    }
}
```

</details>