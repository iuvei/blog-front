<template>
  <div class="animated fadeIn document-detail">

    <div class="row">

      <div class="col-xs-12">
        <div class="pedia-navigation">
          <span class="item active">设计目录</span>
          <span class="tool">
            <router-link class="btn btn-primary btn-sm" :to="'/by/document/edit/'+document.uuid">
              <i class="fa fa-cubes"></i>
              编辑文档
            </router-link>
          </span>
        </div>
      </div>

      <div class="col-xs-12">

        <div class="document-block">

          <div class="title">
            {{document.title}}
          </div>
          <div class="author">
            <MenuFrame :document="document"/>
          </div>

        </div>

      </div>

    </div>

  </div>
</template>

<script>
  import {FeatureType} from '../../common/model/core/FeatureType'
  import NbSwitcher from '../../common/widget/NbSwitcher.vue'
  import NbRadio from '../../common/widget/NbRadio.vue'
  import NbTank from '../../common/widget/NbTank.vue'
  import CreateSaveButton from '../widget/CreateSaveButton'
  import Article from "../../common/model/article/Article";
  import {currentHost} from "../../common/util/Utils";
  import MenuFrame from "./widget/design/MenuFrame"

  export default {

    data() {
      return {
        FeatureType,
        user: this.$store.state.user,
        breadcrumbs: this.$store.state.breadcrumbs,
        document: new Article()
      }
    },
    computed: {
      urlPrefix() {
        return currentHost() + "/a/" + this.user.username + "/"
      }
    },
    components: {
      NbSwitcher,
      NbRadio,
      NbTank,
      CreateSaveButton,
      MenuFrame
    },
    methods: {},
    created() {

    },
    mounted() {
      let that = this
      this.document.uuid = this.$store.state.route.params.uuid
      if (this.document.uuid) {
        this.document.httpDetail(function () {
          that.document.editMode = true
        })
      }
    }
  }
</script>

<style lang="less" rel="stylesheet/less">
  .document-detail {

    .document-block {
      background-color: white;
      box-shadow: 0 0 2px rgba(0, 0, 0, .2);
      border-radius: 5px;
      padding: 20px 15px 10px 15px;
      margin-top: 10px;
      margin-bottom: 30px;

      .title {
        font-size: 22px;
        font-weight: bold;
        text-align: center;
        color: black;
        margin-bottom: 20px;

      }
      .digest {
        text-align: center;
        font-size: 14px;
        margin: 15px;
      }

    }

  }
</style>
