<template>
  <div class="history-overlay">
    <div class="area" @click="onClickArea()" />
    <b-overlay :show="counter === 5" :variant="'dark'" no-wrap>
      <template #overlay>
        <div
          class="d-flex justify-content-start flex-column align-items-center history-overlay-wrapper"
        >
          <button
            v-clipboard:copy="JSON.stringify(histories, null, 2)"
            class="my-3 copy btn btn-sm btn-outline-ets d-flex justify-content-around align-items-center"
          >
            <i class="far fa-clipboard pr-1" />
            {{ $t('Copy') }}
          </button>
          <div class="text-left w-100 pt-0 px-3 pb-3 log-list">
            <small v-for="line in histories" :key="line" class="line d-block">{{
              line
            }}</small>
          </div>
        </div>
      </template>
    </b-overlay>
  </div>
</template>

<script>
import { mapGetters } from 'vuex';

export default {
  name: 'HistoryOverlay',
  data() {
    return {
      counter: 0
    };
  },
  computed: {
    ...mapGetters({
      histories: 'debug/logs'
    })
  },
  methods: {
    onClickArea() {
      if (this.counter++ === 5) this.counter = 0;
    }
  }
};
</script>
