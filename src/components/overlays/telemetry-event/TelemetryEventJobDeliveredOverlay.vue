<template>
  <TelemetryEventBaseOverlay>
    <hr class="m-0 mb-4" />
    <div class="data d-flex justify-content-around align-items-center">
      <div
        class="item px-3 py-1 mx-1 d-flex justify-content-between align-items-center flex-column"
      >
        <span class="title">{{ $t('Delivered time') }}</span>
        <span class="data">{{
          eventRawData.job.deliveryTime
            | $dateTimeLocalized(DATE_FORMAT_SHORT, TIME_FORMAT_SHORT)
        }}</span>
      </div>
      <div
        class="item px-3 py-1 mx-1 d-flex justify-content-between align-items-center flex-column"
      >
        <span class="title">{{ $t('Earned XP') }}</span>
        <span class="data">{{ eventRawData.job.earnedXP }}</span>
      </div>
      <div
        class="item px-3 py-1 mx-1 d-flex justify-content-between align-items-center flex-column"
      >
        <span class="title">{{ $t('Revenue') }}</span>
        <span class="data">{{ unit_currency(eventRawData.job.revenue) }}</span>
      </div>
    </div>
  </TelemetryEventBaseOverlay>
</template>

<script>
import TelemetryEventBaseOverlay from '@/components/overlays/telemetry-event/TelemetryEventBaseOverlay';
import TelemetryEventOverlayMixin from '@/mixins/TelemetryEventOverlayMixin';

export default {
  name: 'TelemetryEventJobDeliveredOverlay',
  components: {
    TelemetryEventBaseOverlay
  },
  mixins: [TelemetryEventOverlayMixin]
};
</script>
