<template>
    <div class="dm-search-entry">
        <b-container fluid class="one">
            <b-icon icon="hash" font-scale="1.5"></b-icon>
            <p style="display: inline">All direct messages</p>
        </b-container>

        <div id="find-user">
            <!-- This is the search box for DM contacts -->
            <b-input-group class="mb-2 d-flex align-items-center">
                <span class="input-label">To:</span>
                <b-form-input
                    class="form-input"
                    v-model="userSearched"
                    @input="searchUser"
                    placeholder="@somebody or somebody@example.com"
                    autofocus
                ></b-form-input>
            </b-input-group>

            <!-- Filtered Dropdrown List of Users -->
            <div
                v-if="filteredUser.length > 0 && userSearched"
                class="user-dropdown"
            >
                <ul>
                    <li
                        v-for="user in filteredUser"
                        v-bind:key="user._iD"
                        @click="changePage"
                    >
                        <img :src="user.image_url" /> {{ user.username }}
                        {{ user.name }}
                    </li>
                </ul>
            </div>
        </div>

        <!-- This div enables me to close the dropdown when I click anywhere outside it -->
        <div @click="closeDropdown" class="close"></div>
    </div>
</template>

<script>
export default {
    prop: {
        component: {
            type: String,
        },
    },
    name: 'SearchDmEntry',
    data() {
        return {
            usersList: [],
            userSearched: '',
            filteredUser: [],
        };
    },

    // drop the API here
    // this.$axios.get('https://dm.zuri.chat/api/v1/get_organization_members')
    // .then(userData => {
    //   console.log(userData)
    //   this.usersList = userData;
    methods: {
        searchUser: function() {
            this.$http
                .get('https://jsonplaceholder.typicode.com/users')
                .then((userData) => {
                    // console.log(userData)
                    this.usersList = userData.data;
                });
            this.filteredUser = this.usersList.filter((user) => {
                if (
                    user.name
                        .toLowerCase()
                        .match(this.userSearched.toLowerCase()) ||
                    user.username
                        .toLowerCase()
                        .match(this.userSearched.toLowerCase())
                )
                    return user;
            });
        },
        closeDropdown: function() {
            this.userSearched = '';
        },
        changePage: function() {
            this.$emit('changePage', 'startDirectMessage');
        },
    },
};
</script>

<style scoped>
* {
    box-sizing: border-box;
}

.dm-search-entry {
    height: 80vh;
    overflow-x: hidden;
    overflow-y: hidden;
}

.one {
    height: 44px;
    background-color: #00b87c;
    color: #fff;
    padding: 0.375rem 1.25rem;
}

.one p {
    font-family: 'Lato', sans-serif;
    font-weight: 700;
    font-size: 1.125rem;
    margin-left: 0.6875rem;
    line-height: 2rem;
}

#find-user {
    height: 58px;
    position: relative;
}

.input-label {
    font-family: 'Lato', sans-serif;
    color: #616061;
    font-weight: 400;
    padding-left: 1.25rem;
}

.form-input {
    height: 61px;
    padding: 1rem;
    border: none;
}

.form-input:focus {
    box-shadow: none;
}

.user-dropdown {
    width: 95%;
    max-height: 279px;
    background-color: #fff;
    margin: 0 auto;
    border-radius: 4px;
    overflow: auto;
    box-shadow: 0px 0px 12px grey;
    position: relative;
    top: -25px;
    /* left: 50%;
    transform: translateX(-50%); */
    z-index: 3;
}

.user-dropdown ul {
    padding: 0;
}

.user-dropdown ul li {
    padding: 0.5rem 1.625rem;
    cursor: pointer;
}

.user-dropdown ul li img {
    width: 21px;
    height: 21px;
    border-radius: 1px;
}

.user-dropdown ul li:hover {
    background-color: #00b87c;
    color: #fff;
}

.close {
    position: absolute;
    inset: 0;
    z-index: -3;
}
</style>
