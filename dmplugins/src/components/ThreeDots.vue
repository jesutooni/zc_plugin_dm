<template>
    <div class="parent position-absolute">
        <div>
            <ul class="child">
                <li><div>Turn off notififcations for replies</div></li>
                <li>
                    <div class="wrapper">
                        <div>Mark Unread</div>
                        <div>
                            <Icon class="icons" icon="healthicons:u" />
                        </div>
                    </div>
                </li>
                <li>
                    <div class="wrapper" @click="toggle">
                        <div>Remind me about this</div>
                        <div>
                            <Icon
                                class="icons"
                                icon="eva:arrow-ios-forward-fill"
                            />
                        </div>
                    </div>
                </li>
                <li><div @click="copy">Copy Link</div></li>
                <li>
                    <div class="wrapper">
                        <div>Pin to this conversation</div>
                        <div>
                            <Icon class="icons" icon="tabler:letter-p" />
                        </div>
                    </div>
                </li>
                <li><div>Turn question into poll</div></li>
                <li>
                    <div class="wrapper">
                        <div>More message shortcuts</div>
                        <div>
                            <Icon class="icons" icon="ri:share-box-line" />
                        </div>
                    </div>
                </li>
            </ul>
        </div>
        <div v-if="load">
            <ul class="load">
                <li><div>In 20 minutes</div></li>
                <li><div>In 1 hour</div></li>
                <li><div>In 3 hours</div></li>
                <li><div>Tomorrow</div></li>
                <li><div>Next week</div></li>
            </ul>
        </div>
    </div>
</template>

<script>
import { Icon } from '@iconify/vue2';
export default {
    name: 'ThreeDots',
    components: {
        Icon,
    },
    data() {
        return {
            Id:
                'https://dm.zuri.chat/api/v1/613b2db387708d9551acee3b/filter_messages',
            load: false,
        };
    },
    methods: {
        toggle() {
            this.load = !this.load;
            console.log('This is a test message');
        },
        copy() {
            this.$http
                .get(
                    'https://dm.zuri.chat/api/v1/copymessagelink/<6145af0d285e4a18402073b20>'
                )
                .then((response) => {
                    this.datas = response.data;
                    console.log(response.data);
                })
                .catch(function(error) {
                    console.log(error);
                });

            alert('Message link is copied');
        },
    },
};
</script>

<style scoped>
.parent {
    font-family: 'Lato', sans-serif;
    font-size: 16px;
    color: #3a3a3a;
    bottom: 1.5rem;
    right: 1rem;
    z-index: 999;
}
.child {
    background-color: #fff;
    box-shadow: 0px 10px 20px rgba(0, 0, 0, 0.18);
    border-radius: 8px;
    width: 344px;
    padding-top: 16px;
    padding-bottom: 16px;
}
.load {
    background-color: #fff;
    box-shadow: 0px 10px 20px rgba(0, 0, 0, 0.18);
    border-radius: 8px;
    width: 160px;
    padding-top: 16px;
    padding-bottom: 16px;
    position: absolute;
    top: 100px;
    left: -150px;
}
ul {
    padding: 0;
}
ul li {
    list-style-type: none;
    padding: 8px;
    padding-left: 34px;
    cursor: pointer;
    transition: all ease-in 0.3s;
}
ul li:hover {
    background: #00b87c;
    color: #fff;
}

ul li:hover .icons {
    color: #fff;
}

.icons {
    font-size: 16px;
    color: #999999;
}
ul li .wrapper {
    display: flex;
    width: 288px;
    justify-content: space-between;
}
</style>
