<template>
  <div class="container">
    <div class="row">

      <div class="col-12 my-2">
        <h3>2 Steps to Reset Your Password</h3>
        <span>2nd Step: Answer the Security Question.</span>
      </div>

      <div class="col-12 my-3">
        <form>

          <div class="my-1 mx-5">

            <div>
              <label for="PWR-Username">Username</label>
            </div>
            <div><h5>User1234</h5></div>


          </div>

          <div class="my-1 mx-5">

            <div>
              <label for="PWR-Email">Security Question</label>
            </div>
            <div><h5>What was your high school mascot?</h5></div>
            <input type="text" placeholder="Answer" id="PWR-Email">

          </div>

          <div class="col-12 my-4">
            <b-link href="#/login"><div class="btn btn-secondary mx-1 mr-5" style="padding:5px 15px;">Cancel</div></b-link>
            <b-link href="#/login"><div href="#/login" class="btn btn-primary mx-1" style="padding:5px 15px;">Continue</div></b-link>
          </div>

        </form>
      </div>

    </div>
  </div>
</template>

<script>
import _ from 'lodash';
import { BounceLoader } from 'vue-spinner/dist/vue-spinner.min.js';
import styles from '@/scss/main.scss';
import CenterCard from '@/components/utils/CenterCard';
import Captcha from '@/components/selfservice/common/Captcha';
import EmailValidation from '@/components/selfservice/common/EmailValidation';
import KbaVerification from '@/components/selfservice/passwordreset2/KbaVerification';
import GenericSelfService from '@/components/selfservice/common/GenericSelfService';
import ResetStage from '@/components/selfservice/passwordreset2/ResetStage';
import SelfserviceAPI from '@/components/selfservice/mixins/SelfserviceAPIMixin';
import UserQuery from '@/components/selfservice/common/UserQuery';

/**
 * @description Selfservice controlling component for recovering a lost password. Makes use of selfservice-reset.json config file.
 *
 * @mixin - selfservice/mixins/SelfserviceAPIMixin.vue
 */
export default {
    name: 'Password-Reset2',
    components: {
        Captcha,
        EmailValidation,
        UserQuery,
        ResetStage,
        kbaSecurityAnswerVerificationStage: KbaVerification,
        GenericSelfService,
        'bounce-loader': BounceLoader,
        'fr-center-card': CenterCard
    },
    data () {
        return {
            selfServiceType: null,
            selfServiceDetails: null,
            loadingColor: styles.baseColor,
            apiType: 'reset'
        };
    },
    mounted () {
        /* istanbul ignore next */
        if (this.$route.params.queryParams) {
            let queryParams = this.parseQueryParams(this.$route.params.queryParams);

            this.advanceStage(queryParams);
        } else {
            this.loadData();
        }
    },
    methods: {
        setChildComponent (type, details) {
            this.selfServiceDetails = details;

            if (type === 'parameters') {
                this.selfServiceType = null;
                this.advanceStage({});
            } else {
                let stageCheck = false;

                _.each(this.$options.components, (value, key) => {
                    if (_.toLower(key) === _.toLower(type)) {
                        stageCheck = true;
                    }
                });

                if (stageCheck) {
                    this.selfServiceType = type;
                } else {
                    this.selfServiceType = 'GenericSelfService';
                }
            }
        },
        apiErrorCallback (error) {
            this.setChildComponent('resetStage', { error: error.response.data.message });
        }
    },
    mixins: [
        SelfserviceAPI
    ]
};
</script>
