<template>
    <transition name="slide">
        <div class="singer-detail"></div>   
    </transition>
</template>

<script>
    import {mapGetters} from 'vuex'
    import {getSingerDetail} from '@/api/singer'
    import {ERR_OK} from '@/api/config'
    import {createSong} from '@/common/js/song'

    export default{
        data(){
            return {
                songs: []
            }
        },
        computed: {
            ...mapGetters([
                'singer'
            ])
        },
        created(){
            this._getDetail()
            
        },
        methods: {
            _getDetail(){
                if(!this.singer.id){
                    this.$router.push('/singer')
                    return
                }
                getSingerDetail(this.singer.id).then((res) => {
                    if(res.code === ERR_OK){
                        this.songs = this._nomalizeSongs(res.data.list)
                        console.log(res.data.list)
                    }
                })
            },
            _nomalizeSongs(list){
                let ret = []
                list.forEach((item) => {
                    let {musicData} = item
                    if(musicData.songid && musicData.albummid){
                        ret.push(createSong(musicData))
                    }
                })
                return ret
            }
        }
    }
</script>

<style lang="scss" scoped>
@import '../../common/styles/variable';

.singer-detail{
    position: fixed;
    z-index: 100;
    top: 0;
    left: 0;
    bottom: 0;
    right: 0;
    background: $color-background
}

.slide-enter-active, .slider-leave-active{
    transition: all .3s;
}

.slide-enter, .slide-leave{
    transform: translate3d(100%, 0, 0);
}
</style>
