<template>
  <TelemetryEventBaseOverlay>
    <hr class="m-0 mb-4" />
    <div class="data d-flex justify-content-around align-items-center">
      <div
        class="item px-3 py-1 mx-1 d-flex justify-content-between align-items-center flex-column"
      >
        <span class="title">{{ $t('Cargo') }}</span>
        <span class="data"
          >{{ (eventRawData.data.cargo * 100) | $toFixed(2) }} %</span
        >
      </div>
      <div
        class="item px-3 py-1 mx-1 d-flex justify-content-between align-items-center flex-column"
      >
        <span class="title">{{ $t('Frame') }}</span>
        <span class="data"
          >{{ (eventRawData.data.chassis * 100) | $toFixed(2) }} %</span
        >
      </div>
    </div>
  </TelemetryEventBaseOverlay>
</template>

<script>
import TelemetryEventBaseOverlay from '@/components/overlays/telemetry-event/TelemetryEventBaseOverlay';
import TelemetryEventOverlayMixin from '@/mixins/TelemetryEventOverlayMixin';

export default {
  name: 'TelemetryEventTrailersDamageOverlay',
  components: {
    TelemetryEventBaseOverlay
  },
  mixins: [TelemetryEventOverlayMixin]
};
</script>
