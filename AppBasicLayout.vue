<script>
import Template from '{Template}/Web/Layout/AppBasic.template'
import JetApplicationMark from '@/Jetstream/ApplicationMark'
import JetBanner from '@/Jetstream/Banner'
import JetDropdown from '@/Jetstream/Dropdown'
import JetDropdownLink from '@/Jetstream/DropdownLink'
import JetNavLink from '@/Jetstream/NavLink'
import JetResponsiveNavLink from '@/Jetstream/ResponsiveNavLink'
import Socket from "@/Jetstream/Socket";
import ThemeMode from "@/Components/ThemeMode";

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
        }
    },
    mounted() {
        // Store user in vuex store
        this.setUser();
        window.TyperSetup();
    },
    methods: {
        setUser() {
            if(this.$page.props.user && !this.$store.getters.getUser) {
                this.$store.dispatch('setUser');
            }
        },
    },
})
</script>
