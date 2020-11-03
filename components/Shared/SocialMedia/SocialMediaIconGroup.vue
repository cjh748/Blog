<template>
    <div>
        <div class="icon-group">
            <FacebookIcon />
            <GithubIcon />
            <InstagramIcon />
            <LinkedInIcon />
            <TwitterIcon />

        </div>
        <div class="icon-group--attribute">
            <p>Icons made by 
                <a href="https://www.flaticon.com/authors/freepik" title="Freepik">
                    Freepik
                </a> 
                from 
                <a href="https://www.flaticon.com/" title="Flaticon"> 
                    www.flaticon.com
                </a>
            </p>
        </div>
    </div>
</template>

<script lang="ts">
import Vue from 'vue';
import FacebookIcon from '../SVGs/FacebookIcon.vue';
import GithubIcon from '../SVGs/GithubIcon.vue';
import InstagramIcon from '../SVGs/InstagramIcon.vue';
import LinkedInIcon from '../SVGs/LinkedInIcon.vue';
import TwitterIcon from '../SVGs/TwitterIcon.vue';

export default Vue.extend({
    name: 'SocialMediaIconGroup',
    components: {
        FacebookIcon,
        GithubIcon,
        InstagramIcon,
        LinkedInIcon,
        TwitterIcon
    }
})
</script>

<style lang="scss">
.icon-group {
    display: flex;
    flex-direction: row;

    &__media-link {
        margin: auto;

        svg {
            width: 25px;
            height: auto;
            
            &:hover {
                path {
                    fill: $color-pacific !important;
                }
            }
        }
    }

    &--attribute {
        margin-top: 8px;
    }
}
</style>