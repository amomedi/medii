<script>
    import Template from '{Template}/Web/Layout/App.template'
    import JetApplicationMark from '@/Jetstream/ApplicationMark'
    import JetBanner from '@/Jetstream/Banner'
    import JetDropdown from '@/Jetstream/Dropdown'
    import JetDropdownLink from '@/Jetstream/DropdownLink'
    import JetNavLink from '@/Jetstream/NavLink'
    import JetResponsiveNavLink from '@/Jetstream/ResponsiveNavLink'
    import Socket from "@/Jetstream/Socket";
    import ThemeMode from "@/Components/ThemeMode";
    import moment from "moment";

    export default Template({
        components: {
            Socket,
            JetApplicationMark,
            JetBanner,
            JetDropdown,
            JetDropdownLink,
            JetNavLink,
            JetResponsiveNavLink,
            ThemeMode
        },

        computed: {
            logo() {
                return this.$page.props.siteLogo
            },
            isHomePage() {
                return this.$page.props.isHome;
            },
            isMarketPage() {
                return this.$page.props.isMarket;
            },
            time() {
                return this.currentTime;
            }
        },
        beforeDestroy: function(){

            window.removeEventListener('resize', this.mq)

            clearInterval( this.timeInterval )
        },
        created() {

            window.addEventListener('resize', this.mq)

            let format = 'YYYY-MM-DD HH:mm:ss Z';

            this.currentTime = moment().format(format);

            this.timeInterval = setInterval(() => {
                this.currentTime = moment().format(format);
            }, 1000)
        },
        data() {
            return {
                timeInterval: null,
                currentTime: null,
                showingUserProfileDropdown: false,
                showingNavigationDropdown: false,
                showingSettingsDropdown: false,
                menuToggled: false,
                isMobile: false
            }
        },
        mounted() {
          this.mq();
          this.setUser();
        },
        methods: {
            mq () {
                if (typeof window.matchMedia !== "undefined") {
                    this.isMobile = window.matchMedia('(max-width: 1000px)').matches;
                }
            },
            setUser() {
                if(this.$page.props.user && !this.$store.getters.getUser) {
                    this.$store.dispatch('setUser');
                }
            },
            isUrl(urls) {
                let currentUrl = this.$page.url.substr(1).split('/');
                if(currentUrl[0]) {
                    return currentUrl[0].startsWith(urls)
                }
            },
            setProfile() {
                this.$inertia.visit(route('login'));
            }
        },
    })
</script>
