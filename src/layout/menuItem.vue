<template>
    <div class="menuItem">
        <template v-for="(list,listIndex) in json">
            <!-- 有子路由的 -->
            <el-submenu v-if="list.children && list.children.length > 0" :index="list.name" :key="listIndex">
                <template slot="title">
                    <i v-if="list.icon" :class="list.icon"></i>
                    <span slot="title">{{list.title}}</span>
                </template>
                <template v-for="(item,itemIndex) in list.children" >
                    <!-- 子路由里还有子路由的 -->
                    <my-menu-item v-if="item.children && item.children.length > 0" :json="[item]"></my-menu-item>

                    <!-- 子路由里没有子路由的 -->
                    <router-link v-else :to="{name: item.name}">
                        <el-menu-item  :index="item.name" :key="itemIndex">
                            <i v-if="item.icon" :class="item.icon"></i>{{item.title}}
                        </el-menu-item>
                    </router-link>
                </template>
            </el-submenu>

            <!-- 没有子路由的 -->
            <router-link v-else :to="{name: list.name}">
                <el-menu-item :index="list.name" :key="listIndex">
                    <i v-if="list.icon" :class="list.icon"></i>
                    <i v-if="list.padding" style="padding-left: 32px"></i>
                    <span slot="title">{{list.title}}</span>
                </el-menu-item>
            </router-link>
        </template>
    </div>

</template>
<script>
export default {
    name: 'menuItem',
    props: {
        json: Array
    }
}
</script>
<style lang='stylus'>
.menuItem {
    a{
        display: block;
    }
}
</style>
