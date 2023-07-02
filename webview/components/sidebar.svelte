<script async>
    window.addEventListener("DOMContentLoaded", () => {
        function selectIconType(e) {
            e.target.style.color = "red";
        }

        // selecting all types buttons
        let iconTypes = document.getElementsByClassName("icon-types");

        // assigning onClick function
        for (const btn of iconTypes) {
            btn.addEventListener("click", selectIconType);
        }
    });
</script>

<body>
    <header>
        <ul>
            <li class="icon-types" id="mui">MUI</li>
            <li class="icon-types" id="fa">FA</li>
            <li class="icon-types" id="bootstrap">BT</li>
        </ul>
    </header>
    <nav>
        <div class="select-version-and-search">
            <div class="search">
                <input type="text" name="search" id="search" />
            </div>
            <div class="select-version">
                <label for="select-version">v: &nbsp;</label>
                <select name="select-version" id="select-version">
                    <option value="4.56.5">4.56.5</option>
                    <option value="4.56.5">4.56.5</option>
                    <option value="4.56.5">4.56.5</option>
                    <option value="4.56.5">4.56.5</option>
                    <option value="4.56.5">4.56.5</option>
                </select>
            </div>
        </div>
    </nav>
    <section>
        
    </section>
</body>

<style>
    body {
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
        margin: 0.5rem 0.4rem !important;
        padding: 0.4rem 1.2rem !important;
        box-shadow: rgba(245, 222, 179, 0.346) 0 0 3px 2px;
        font-weight: 500;
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
        justify-content: space-around;
        padding: 0.5rem 0.5rem !important;
    }

    /*  */
    body nav .select-version-and-search .search {
        width: 60% !important;
        display: flex;
    }
    
    body nav .select-version-and-search .select-version {
        width: 35% !important;
        display: flex;
        align-items: center;
        font-size: larger;
    }
    /*  */
    
    body nav .select-version-and-search .search input {
        min-width: 3rem !important;
        width: 100%;
        font-weight: 500 !important;
    }
    body nav .select-version-and-search .select-version select {
        width: 70%;
    }
    
    
    body nav .select-version-and-search .select-version label {
        font-size: larger;
        font-weight: 400;
    }
    
    body nav .select-version-and-search .select-version select {
        font-size: larger;
    }
</style>
