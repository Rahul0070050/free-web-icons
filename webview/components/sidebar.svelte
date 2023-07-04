<script async>
    import FAIcons from "../media/data/fa-icons.json";
    import iconVersions from "../media/data/versions.json";

    // global variables
    let selectedIconVersion = iconVersions.versions[0];
    let iconInfo = FAIcons[0]
    window.addEventListener("DOMContentLoaded", () => {

        // selecting DOM elms
        const messageText = document.getElementById("message-text");
        const iconVersionSelector = document.getElementById("select-version");
        const copyBtn = document.querySelector(".copy-cdn-link-btn");
        const iconListContainer = document.getElementById("icon-list");
        const searchInput = document.getElementById("search");
        let search = ""

        copyBtn.addEventListener("click", copyText);

        async function copyText (e) {
            console.log(e.target.getAttribute("data-attar"));
            let message = ""
            let content = ""
            if(e.target.getAttribute('data-attar') == 'cdn-copy-btn') {
                content = iconInfo.cdn
                message = "CDN copied"
            }else {
                content = `<i class='${e.target.getAttribute("data-attar")}'></i>`
                message = "icon copied"
            }

            await navigator.clipboard.writeText(content);

            messageText.innerText = message

            messageText.style.zIndex = '11'
            messageText.style.opacity = '11'


            setTimeout(() => {
                messageText.style.zIndex = '-1'
                messageText.style.opacity = '0'
            }, 1000);
        }

        showIcons(iconVersions.versions[0]);
        showVersions();

        console.log(searchInput);

        searchInput.addEventListener('input',(e) => {
            search = e.target.value;
            showIcons(selectedIconVersion);
        })

        function showVersions() {
            iconVersionSelector.innerHTML = "";
            iconVersions.versions.forEach((v) => {
                iconVersionSelector.innerHTML += `<option value=${v}>v:${v}</option>`;
            });
        }

        
        function showIcons(version) {
            iconInfo = FAIcons.find((icons) => icons.version == version);
            
            iconListContainer.innerHTML = ``
                
            iconInfo.icons.map(icon => {
                console.log(search != "");
                console.log(search);
                if(search != "") {
                    if(!icon.name.startsWith(search)) {
                        return null
                    }
                }
                let iTag = document.createElement('i');
                iTag.setAttribute("class",`${icon.showIcon} svelte-1p5v1u4`);
                iTag.setAttribute("data-attar",`${icon.showIcon}`);
                iTag.setAttribute("title", icon.name);
                iTag.addEventListener('click',copyText)
                iconListContainer.appendChild(iTag)
            })
            // `<i class="fa-solid fa-house" title="home" />`
        }

        
        iconVersionSelector.addEventListener("change", (e) => {
            selectedIconVersion = e.target.value;
            showIcons(selectedIconVersion);
        });
    });
</script>

<body>
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
            <div class="icons-container">
            <div class="icon-list" id="icon-list">
            </div>
        </div>
    </section>
    <div id="message-text"></div>
</body>

<style>
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
