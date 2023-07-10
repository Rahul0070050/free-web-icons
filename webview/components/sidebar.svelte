<script async>
    import FAIcons from "../media/data/fa-icons.json";
    import iconVersions from "../media/data/versions.json";
    import {fly} from "svelte/transition";

    // global variables
    let selectedIconVersion = iconVersions.versions[0];
    let iconInfo = FAIcons[0]
    let search = ""
    let size = ""
    let rotation = ""
    let animation = ""
    let color = "#cccccc"
    let selectedIcon = ""
    let selectedIconName = ""
    window.addEventListener("DOMContentLoaded", (e) => {

        // selecting DOM elms
        const messageText = document.getElementById("message-text");
        const iconVersionSelector = document.getElementById("select-version");
        const copyBtn = document.querySelector(".copy-cdn-link-btn");
        const iconListContainer = document.getElementById("icon-list");
        const searchInput = document.getElementById("search");

        window.copyText = async function copyText(e) {
            console.log(e.target.getAttribute("data-attar"));
            let message = ""
            let content = ""
            if(e.target.getAttribute('data-attar') == 'cdn-copy-btn') {
                content = iconInfo.cdn
                message = "CDN copied"
            }else {
                content = `<i class="${selectedIcon} ${size && size} ${rotation && rotation} ${animation && animation}" style="color: ${color};" />`
                message = "icon copied"
            }
            
            await window.navigator.clipboard.writeText(message)
    
            messageText.innerText = message
    
            messageText.style.zIndex = '11'
            messageText.style.opacity = '11'
    
    
            setTimeout(() => {
                messageText.style.zIndex = '-1'
                messageText.style.opacity = '0'
            }, 1000);
        }
        
        window.openIconInfo = async function openIconInfo (e) {
        }

        window.openIconInfo = function openIconInfo(e) {
            console.log(e.target);
            selectedIcon = e.target.getAttribute('data-attar')
            selectedIconName = e.target.getAttribute('title').replace('-',' ').toUpperCase()
        }

        showVersions();
        showIcons(iconVersions.versions[0]);

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
            
            // iconListContainer.innerHTML = ``

            iconInfo?.icons?.map((icon,i) => {
                if(search != "") {
                    if(!icon.name.startsWith(search)) {
                        return null
                    }
                }

                let iTag = document.createElement('i');
                iTag.setAttribute("class",`${icon.showIcon} svelte-1wf2oa9`);
                iTag.setAttribute("data-attar",`${icon.showIcon}`);
                iTag.setAttribute("title", icon.name);
                iTag.addEventListener('click',openIconInfo)
                iconListContainer.appendChild(iTag)
            })
            // `<i class="fa-solid fa-house" title="home" />`
        }
        
        
        
        iconVersionSelector.addEventListener("change", (e) => {
            selectedIconVersion = e.target.value;
            showIcons(selectedIconVersion);
        });
    });

    function openIconInfo(e) {
        window.openIconInfo(e)
    }

    function copyText(e) {
        window.copyText(e)
    }

    function selectedFilter(e) {
        console.log(e.target.name);
        console.log(e.target.value);

        if(e.target.name == "color") {
            color = e.target.value
        }
        if(e.target.name == "size") {
            size = e.target.value
        }
        if(e.target.name == "rotate") {
            rotation = e.target.value
        }
        if(e.target.name == "animate") {
            animation = e.target.value
        }
    }


    function  closeIconInfoWindow() {
        selectedIcon = ""
        size = ""
        rotation = ""
        animation = ""
    }
    
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
            <span data-attar="cdn-copy-btn" class="copy-cdn-link-btn" on:click={copyText}>
                <i data-attar="cdn-copy-btn" class="fa-solid fa-link" />
            </span>
        </div>
    </nav>
    <section class="list-icons">
        <div class="icons-container">
            <div class="icon-list" id="icon-list">
                <i class="fa-solid fa-house" title="home" />
            </div>
            {#if selectedIcon != "" }
                <div class="icon-info-container" transition:fly={{y: -20}}>
                    <div class="headder">
                        <h3>{selectedIconName}</h3> <i on:click={closeIconInfoWindow} class="fa-solid fa-xmark"></i>
                    </div>
                    <div class="icon-preview">
                        <i class="{selectedIcon} {size} {animation} {rotation}" style="color: {color};" title="home" on:click={copyText} />
                    </div>
                    <div class="actions">
                        <div class="form-control">
                            <input type="color" value="#cccccc" name="color" id="color" on:change={selectedFilter}>
                        </div>
                        <div class="form-control">
                            <label for="size">size</label>
                            <select name="size" id="size" on:click={selectedFilter}>
                                <option value="none">none</option>
                                <option value="fa-sm">sm</option>
                                <option value="fa-gl">gl</option>
                                <option value="fa-xl">xl</option>
                                <option value="fa-2xl">2xl</option>
                            </select>
                        </div>
                        <div class="form-control">
                            <label for="rotate">rotate</label>
                            <select name="rotate" id="rotate" on:click={selectedFilter}>
                                <option value="">none</option>
                                <option value="fa-rotate-90">rotate 90</option>
                                <option value="fa-rotate-180">rotate 180</option>
                                <option value="fa-rotate-270">rotate 90</option>
                                <option value="fa-flip-horizontal">flip horizontal</option>
                                <option value="fa-flip-both">flip vertical</option>
                            </select>
                        </div>
                        <div class="form-control">
                            <label for="animation">animate</label>
                            <select name="animate" id="animate" on:click={selectedFilter}>
                                <option value="">none</option>
                                <option value="fa-beat">beat</option>
                                <option value="fa-beat-fade">beat & fade</option>
                                <option value="fa-bounce">bounce</option>
                                <option value="fa-fade">fade</option>
                                <option value="fa-flip">flip</option>
                                <option value="fa-spin">spin</option>
                                <option value="fa-shake">shake</option>
                                <option value="fa-spin-pulse">spin pulse</option>
                            </select>
                        </div>
                    </div>
                    <div class="copy" on:click={copyText}>
                        <span>copy</span>
                    </div>
                </div>
            {/if}
        </div>
    </section>
    <div id="message-text"></div>
</body>

<style>
    body {
        position: relative;
    }
    body nav {
        width: 100% !important;
        display: flex;
        align-items: center;
        justify-content: center;
    }
    body nav .select-version-and-search {
        max-width: 17.5rem;
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
        max-width: 17.5rem;
    }
    body section .icons-container .icon-list i {
        cursor: pointer;
        font-size: medium;
        padding: 0.7rem !important;
        margin: 0.1rem !important;
        width: 2.5rem;
        box-shadow: inset rgba(245, 222, 179, 0.346) 0 0 3px 2px;
    }
    body section .icon-info-container {
        max-width: 16rem;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%,-50%);
        height: fit-content;
        width:  95%;
        margin: 0.3rem 0 !important;
        padding: 1rem 0 !important;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        box-shadow: inset  0 0 2px 2px rgba(173, 216, 230, 0.269);
        background-color: black;
    }
    body section .icon-info-container .headder {
        display: flex;
        align-items: center;
        justify-content: space-between;
        width: 100%;
        padding: 0.1rem 1rem 1rem 1rem !important;
    }
    body section .icon-info-container .headder i {
        padding: 0.4rem 0.5rem !important;
        border: 1px solid rgba(255, 255, 255, 0.542);
        color: rgba(255, 255, 255, 0.512);
        border-radius: 4px;
        transition: all 0.3s ease;
    }
    body section .icon-info-container .headder i:hover {
        border-color: white;
        color: white;
    }
    body section .icon-info-container .icon-preview{
        border: 1px solid rgba(245, 222, 179, 0.317);
        width: 90%;
        height: 10rem;
        display: flex;
        align-items: center;
        justify-content: center;
    }
    body section .icon-info-container .icon-preview i {
        cursor: pointer;
        box-shadow: none;
    }
    body section .icon-info-container .actions {
        display: flex;
        flex-direction: column;
        align-items: center;
        width: 90% !important;
        padding: 1rem 0 !important;
    }
    body section .icon-info-container .actions .form-control {
        display: flex;
        flex-direction: column;
        width: 100% !important;
        padding: 0.2rem 0 !important;
    }
    /* body section .icon-info-container .actions .form-control select:se */
    body section .icon-info-container .actions .form-control label {
        font-size: larger;
        text-transform: capitalize;
        padding: 0.3rem 0.1rem !important;
    }

    /* remove down arrow from dropdown */
    body section .icon-info-container .actions .form-control select {}
    /* remove down arrow from dropdown */

    body section .icon-info-container .actions .form-control select {
        padding: 0.2rem !important;
        border-radius: 4px;
        font-size: larger;
        color: black;
    }
    body section .icon-info-container .actions .form-control input {
        font-size: x-large !important;
    }
    body section .icon-info-container .actions .form-control select,
    body section .icon-info-container .actions .form-control input {
        width: 100% !important;
    }
    .copy {
        padding: 0.4rem 0.5rem !important;
        width: 90%;
        color: black;
        text-align: center;
        font-size: larger;
        background-color: lemonchiffon;
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
