<template>
    <ul class="pagination">
        <li :class="{disabled:!link.active , active:link.active}" v-for="(link,key) in links">
            <a :class="{ active:link.active}" @click.prevent="goToPage(link.url)" :href="link.url" v-if="link.url"
               v-html="prevNextHtml(key,link.label)"></a>
            <span v-else v-html="prevNextHtml(key,link.label)"></span>
        </li>
    </ul>
</template>

<script>
export default {
    name: "vue-pagination",
    props: {
        links: {
            type: Array,
            default: function () {
                return []
            }
        },
        prevHtml: {
            type: String,
            default: '<i class="icon icon-prev"></i>'
        },
        nextHtml: {
            type: String,
            default: '<i class="icon icon-next-active"></i>'
        }
    },
    methods: {
        prevNextHtml(key, label) {
            if (key === 0) return this.prevHtml
            else if (key === this.links.length-1) return this.nextHtml
            else return label
        },
        goToPage(url) {
            this.$emit('change', {
                url: url,
                page: parseInt(this.getUrlParameter(url, 'page'))
            })
        },
        getUrlParameter(url, name) {
            name = name.replace(/[\[]/, '\\[').replace(/[\]]/, '\\]');
            var regex = new RegExp('[\\?&]' + name + '=([^&#]*)');
            var results = regex.exec(url);
            return results === null ? '' : decodeURIComponent(results[1].replace(/\+/g, ' '));
        }
    }
}
</script>

<style scoped>

</style>
