<template>
   <div class="container">
        <h2 class="search-title">Search</h2>
        <div class="search-box-container">
            <input v-model="searchTerm" type="text" placeholder="Type to search..." class="search-box"/>
            <span v-if="searchTerm" >
                <svg class="clear-icon" @click="clearSearch" width="16px" height="16px" view-box="0 0 16 16" fill="currentColor">
                    <path d="M4 4L12 12M12 4L4 12" stroke="black" stroke-width="2" stroke-linecap="round"/>
                </svg>
            </span>
        </div>
        <p class="results-count">
            <strong>{{ filteredArticles.length }}</strong>
            posts found.
        </p>

        <div v-for="(article, index) in filteredArticles" :key="index" class="article-card">
            <h3 v-html="highlightText(article.title)" class="article-title"></h3>
            <p class="article-date">{{article.date  }}</p>
            <p class="article-content" v-html="highlightText(article.content)"></p>
        </div>
   </div> 
</template>

<script>
import articlesData from "@/data/articlesData.js"
export default {
    data() {
        return {
            searchTerm: "",
            articles: articlesData
        };
    },
    computed: {
        filteredArticles() {
            if(!this.searchTerm) return this.articles;

            return this.articles.filter(
                (article) => article.title.toLowerCase().includes(this.searchTerm.toLowerCase()) || article.content.toLowerCase().includes(this.searchTerm.toLowerCase())
            );
        },
    },
    methods: {
        highlightText(text) {
            if(!this.searchTerm) return text;

            const regex = new RegExp(`(${this.searchTerm})`, "gi");
            return text.replace(regex, `<span class="highlight">$1</span>`)
        },
        clearSearch() {
            this.searchTerm = "";
        }
    }
}
</script>

<style scoped>
.container {
    max-width: 800px;
    margin: auto;
    padding: 20px;
    font-family: Arial, Helvetica, sans-serif;
}
.search-title {
    font-size: 24px;
    color: #333;
}
.search-box {
    width: 96%;
    padding: 12px;
    font-size: 16px;
    margin-bottom: 10px;
    border: 2px solid #007BFF;
    border-radius: 5px;
    outline: none;
    transition: border 0.3s;
}
.search-box:focus {
    border-color: #0056b3;
}

.search-box-container {
    position: relative;
    width: 100%;
}
.clear-icon {
    position: absolute;
    right: 20px;
    top: 26%;
    font-size: 18px;
    cursor: pointer;
    color: #888;
    transition: color 0.3s;
}
.article-card {
    background-color: #f9f9f9;
    padding: 15px;
    border-radius: 8px;
    box-shadow: 0px 4px 6px rgba(0,0,0,0.1);
    margin-bottom: 15px;
    transition: transform 0.2s;
}
.article-card:hover {
    transform: scale(1.02);
}
.article-title {
    color: #007bff;
    margin-bottom: 5px;
}
.article-date {
    font-size: 14px;
    color: #888;
}
.article-content {
    font-size: 16px;
    color: #444;
}
</style>