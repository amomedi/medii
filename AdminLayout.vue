<script>
import Template from '{Template}/Admin/Layout/App.template'
import JetApplicationMark from '@/Jetstream/ApplicationMark'
import JetBanner from '@/Jetstream/Banner'
import JetDropdown from '@/Jetstream/Dropdown'
import JetDropdownLink from '@/Jetstream/DropdownLink'
import JetNavLink from '@/Jetstream/NavLink'
import JetResponsiveNavLink from '@/Jetstream/ResponsiveNavLink'
import NavLink from "@/Jetstream/NavLink";
import Socket from "@/Jetstream/Socket";

export default Template({
    components: {
        Socket,
        NavLink,
        JetApplicationMark,
        JetBanner,
        JetDropdown,
        JetDropdownLink,
        JetNavLink,
        JetResponsiveNavLink,
    },

    computed: {
        logo() {
            return this.$page.props.siteLogo
        }
    },

    data() {
        return {
            open: false,
            showingNavigationDropdown: false,
        }
    },
    updated() {

    },
    methods: {
        switchToTeam(team) {
            this.$inertia.put(route('current-team.update'), {
                'team_id': team.id
            }, {
                preserveState: false
            })
        },

        logout() {
            this.$inertia.post(route('logout'));
        },
        isUrl(urls) {

            let currentUrl = this.$page.url.substr(1).split('/');

            if (urls === 'dashboard' && !currentUrl[1]) {
                return true;
            }

            if(currentUrl[1]) {
                return currentUrl[1].startsWith(urls)
            }
        },
    }
})
</script>
