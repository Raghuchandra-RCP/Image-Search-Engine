# Image-Search-Engine
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Image Search Engine</title>
    <style>
        /* Your CSS styles go here */
        body {
            font-family: poppins, sans-serif;
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            background: #39297b;
            color: #fff;
        }

        h1 {
            text-align: center;
            margin: 100px auto 50px;
            font-weight: 600;
        }

        form {
            width: 90%;
            max-width: 600px;
            height: 80px;
            display: flex;
            align-items: center;
            margin: auto;
            background: rgb(67, 73, 137);
            border-radius: 8px;
        }

        form input {
            height: 100%;
            color: rgb(255, 255, 255);
            font-size: 18px;
            flex: 1 1 0%;
            border-width: 0;
            border-style: initial;
            border-color: initial;
            border-image: initial;
            outline: 0;
            background: transparent;
            padding: 0px 30px;
        }

        form button {
            height: 100%;
            color: rgb(255, 255, 255);
            font-size: 18px;
            border-top-right-radius: 8px;
            border-bottom-right-radius: 8px;
            cursor: pointer;
            padding: 0 40px;
            background: rgb(255, 57, 41);
            border-width: 0;
            border-style: initial;
            border-color: initial;
            border-image: initial;
            outline: 0;
        }

        #show-more-btn {
            color: rgb(255, 255, 255);
            cursor: pointer;
            display: block;
            background: rgb(255, 57, 41);
            border-width: 0;
            border-style: initial;
            border-color: initial;
            border-image: initial;
            outline: 0;
            padding: 10px 20px;
            border-radius: 4px;
            margin: 10px auto 100px;
        }

        ::placeholder {
            color: #fff;
            font-size: 18px;
        }

        .search-result {
            width: 80%;
            margin: 100px auto 50px;
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 20px;
        }

        .search-result img {
            width: 100%;
            height: 230px;
            object-fit: cover;
            border-radius: 5px;
        }
    </style>
</head>
<body>
    <h1>Image Search Engine</h1>
    <form id="search-form">
        <input type="text" id="search-box" placeholder="Search anything here...">
        <button>Search</button>
    </form>
    <div class="search-result"></div>
    <button id="show-more-btn">Show more</button>
    <script>
        const accessKey = "UZbUoVYBo-lM_sTQsRBTwnXniWClE-WRC56CyLIXB9c"

        const searchform = document.getElementById("search-form");
        const searchbox = document.getElementById("search-box");
        const searchResult = document.querySelector(".search-result");
        const showmorebtn = document.getElementById("show-more-btn");

        let keyword = "";
        let page = 1;

        async function searchImages() {
            keyword = searchbox.value;
            const url = `https://api.unsplash.com/search/photos?page=${page}&query=${keyword}&client_id=${accessKey}&per_page=20`;

            const response = await fetch(url);
            const data = await response.json();

            if(page == 1){
                searchResult.innerHTML = "";
            }
            const results = data.results;

            results.map(result => {
                const image = document.createElement("img");
                image.src = result.urls.regular;

                const imageLink = document.createElement("a");
                imageLink.href = result.links.html;
                imageLink.target = "_blank";

                imageLink.appendChild(image);
                searchResult.appendChild(imageLink);
            });
            showmorebtn.style.display = "block";
        }

        searchform.addEventListener("submit", (e) => {
            e.preventDefault();
            page = 1;
            searchImages();
        });

        showmorebtn.addEventListener("click",() => {
            page++;
            searchImages();
        });
    </script>
</body>
</html>
