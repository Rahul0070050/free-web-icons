<script async>
    import FAIcons from "../media/data/icons/fa.json";
    import BTIcons from "../media/data/icons/bt.json";
    import MUIIcons from "../media/data/icons/mui.json";
    import iconVersions from "../media/data/versions.json";

    // global variables
    let selectedIconTypes = "FA";
    let selectedIconVersion = iconVersions["FA"].versions[0];
    let iconInfo = FAIcons[0]
    window.addEventListener("DOMContentLoaded", () => {
        iconInfo = FAIcons[0]
        // selecting DOM elms
        let iconTypes = document.getElementsByClassName("icon-types");
        const iconTypeName = document.getElementById("icon-type-name");
        const messageText = document.getElementById("message-text");
        const iconVersionSelector = document.getElementById("select-version");
        const copyBtn = document.querySelector(".copy-cdn-link-btn");
        const iconListContainer = document.getElementById("icon-list");

        // if (typeof(Worker) !== "undefined") {
        //     console.log('yes');
        // } else {
        //     console.log('no');
        // }

        for (const btn of iconTypes) {
            btn.addEventListener("click", selectIconType);
        }

        copyBtn.addEventListener("click", async (e) => {
            let message = ""
            console.log(e.target);
            if(e.target.getAttribute('data-attar') == 'cdn-copy-btn')
                message = "CDN copied"
            else
                message = "icon copied"

            await navigator.clipboard.writeText("hi");

            messageText.innerText = message
            messageText.style.zIndex = '11'
            messageText.style.opacity = '11'


            setTimeout(() => {
                // messageText.classList.remove('show-message')
                messageText.style.zIndex = '-1'
                messageText.style.opacity = '0'
            }, 1000);
        });

        showIcons(iconVersions[selectedIconTypes].versions[0], selectedIconTypes);
        showVersions();

        iconTypes[0].style.boxShadow =
            "inset rgba(245, 222, 179, 0.346) 0 0 3px 2px";
        iconTypes[0].style.transform = "scale(1.1)";
        iconTypeName.innerText = "FA";

        function selectIconType(e) {
            for (const btn of iconTypes) {
                if (e.target.getAttribute("id") == btn.getAttribute("id")) {
                    selectedIconTypes = e.target.getAttribute("id");

                    iconTypeName.innerText = selectedIconTypes;

                    showVersions();
                    showIcons(iconVersions[selectedIconTypes].versions[0], selectedIconTypes);

                    btn.style.boxShadow =
                        "inset rgba(245, 222, 179, 0.346) 0 0 3px 2px";
                    btn.style.transform = "scale(1.1)";
                    btn.style.fontWeight = "500";
                } else {
                    btn.style.boxShadow =
                        "rgba(245, 222, 179, 0.346) 0 0 1px 1px";
                    btn.style.transform = "scale(1)";
                }
            }
        }

        function showVersions() {
            iconVersionSelector.innerHTML = "";
            iconVersions[selectedIconTypes].versions.forEach((v) => {
                iconVersionSelector.innerHTML += `<option value=${v}>v:${v}</option>`;
            });
        }

        function showIcons(version, iconType) {
            switch (iconType) {
                case "FA":
                    iconInfo = FAIcons.find((icons) => icons.version == version);
                    break;
                case "BT":
                    iconInfo = BTIcons.find((icons) => icons.version == version);
                    break;
                case "MUI":
                    iconInfo = MUIIcons.find((icons) => icons.version == version);
                    break;
                default:
                    break;
            }
            iconListContainer.innerHTML += ``
            // iconInfo.icons.map(icon => {
            //     let iTag = document.createElement('i');
            //     iTag.setAttribute("class",icon.showIcon);
            //     iTag.setAttribute("title",icon.name);
            //     iTag.style.cursor = 'pointer !important';
            //     iTag.style.padding = '0.9rem !important';
            //     iTag.style.margin = '0.1rem !important';
            //     iTag.style.boxShadow = 'inset rgba(245, 222, 179, 0.346) 0 0 3px 2px !important';
            //     iconListContainer.appendChild(iTag)
            // })
            // `<i class="${icon.showIcon}" title="${icon.name}" />`
        }

        iconVersionSelector.addEventListener("change", (e) => {
            selectedIconVersion = e.target.value;
            showIcons(selectedIconVersion, selectedIconTypes);
        });

    });
    
    function handleClick(e) {
        console.log(e);
    }
</script>

<body>
    <header>
        <ul>
            <li class="icon-types" id="FA">FA</li>
            <li class="icon-types" id="MUI">MUI</li>
            <li class="icon-types" id="BT">BT</li>
        </ul>
    </header>
    <nav>
        <div class="select-version-and-search">
            <div class="search">
                <input type="text" name="search" id="search" />
            </div>
            <div class="select-version">
                &nbsp;
                <!-- <label for="select-version">v: &nbsp;</label> -->
                <select name="select-version" id="select-version" />
            </div>
            <span data-attar="cdn-copy-btn" class="copy-cdn-link-btn">
                <i data-attar="cdn-copy-btn" class="fa-solid fa-link" />
            </span>
        </div>
    </nav>
    <section class="list-icons">
        <strong><span id="icon-type-name" /> icons</strong>
        <div class="icons-container">
            <div class="icon-list" id="icon-list">
                {#each iconInfo.icons as icon, _}
                    <i class="{icon.showIcon}" on:click="{handleClick(icon.showIcon)}"></i>
                {/each}
            </div>
        </div>
    </section>
    <div id="message-text"></div>
</body>

<style>
    body {
        position: relative;
        height: 100vh;
        background-color: #181818;
    }
    body header ul {
        overflow-x: auto;
        list-style: none;
        display: flex;
        justify-content: start;
        margin: 1rem;
    }

    body header ul::-webkit-scrollbar {
        display: none;
    }

    body header ul li {
        cursor: pointer;
        margin: 0.5rem 0.4rem !important;
        padding: 0.3rem 1.1rem !important;
        box-shadow: rgba(245, 222, 179, 0.346) 0 0 3px 2px;
    }

    body header ul li:first-child {
        margin-left: 0.5rem !important;
    }

    body header ul li:last-child {
        margin-right: 0.5rem !important;
    }

    body nav .select-version-and-search {
        width: 100% !important;
        display: flex;
        align-items: center;
        justify-content: space-around;
        padding: 0.5rem 0.3rem !important;
    }

    /*  */
    body nav .select-version-and-search .search {
        width: 67% !important;
        display: flex;
    }

    body nav .select-version-and-search .select-version {
        width: 30% !important;
        display: flex;
        align-items: center;
    }
    /*  */

    body nav .select-version-and-search .search input {
        min-width: 3rem !important;
        width: 100%;
        font-weight: 500 !important;
    }
    body nav .select-version-and-search .select-version select {
        width: 90%;
    }

    /* toot tip */
    body nav .select-version-and-search .copy-cdn-link-btn:hover::-ms-tooltip {
        content: "hi";
    }
    /* toot tip */

    body nav .select-version-and-search .copy-cdn-link-btn {
        height: 1.2rem !important;
        width: 1.3rem !important;
        display: flex;
        cursor: pointer;
        justify-content: center;
        align-items: center;
        box-shadow: inset rgba(245, 222, 179, 0.346) 0 0 3px 2px;
    }
    body section strong {
        text-transform: capitalize;
        margin: 1rem !important;
    }

    body section .icons-container::-webkit-scrollbar {
        display: none;
    }
    body section .icons-container {
        height: 85vh;
        overflow-y: auto;
        display: flex;
        justify-content: center;
        margin-top: 0.5rem !important;
    }
    body section .icons-container .icon-list {
        width: 90%;
    }
    body section .icons-container .icon-list i {
        cursor: pointer;
        padding: 0.9rem !important;
        margin: 0.1rem !important;
        box-shadow: inset rgba(245, 222, 179, 0.346) 0 0 3px 2px !important;
    }
    body #message-text {
        position: absolute;
        background-color: white;
        border-radius: 25px;
        left: 50%;
        color: black;
        transform: translate(-50%, -50%);
        padding: 0.5rem 1rem !important;
        border: 1px solid lightcyan;
        text-align: center;
        bottom: 0;
        opacity: 0;
        z-index: 0;
        transition: all ease 0.5s;
    }
</style>
