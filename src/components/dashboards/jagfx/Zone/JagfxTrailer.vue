<template>
  <div class="trailer capitalized">
    <div class="t-info">
      <div class="trailer-data">
        <!--<span>{{bodyType}}</span>
				<small>{{chainType}}</small>-->
        <div v-if="$hasTrailerAndJob()" class="job">
          {{ telemetry.job.cargo.name }}
        </div>
        <div v-else-if="$hasTrailer()" class="job disabled">
          <i>-- {{ $t('No Job') }} --</i>
        </div>
        <div v-else class="job disabled">
          <i>-- {{ $t('No trailer') }} --</i>
        </div>
      </div>
      <div class="job-data">
        <small class="licencePlate left">
          <span class="flag">
            {{
              $flag(
                telemetry.trailer.licensePlate.country.id,
                telemetry.game.game.id
              )
            }}
          </span>
          <span v-if="$hasTrailer()" class="w-100 text-center">
            <span>{{ telemetry.trailer.licensePlate.value }}</span>
          </span>
          <span v-else class="w-100 text-center">{{ $t('N/A') }}</span>
        </small>
        <div v-if="$hasTrailer()" class="damage left">
          {{ $trailerDamage() }} %
        </div>
        <div v-else class="damage left">
          {{ $t('N/A') }}
        </div>
      </div>
      <!--<div class="trailer-wear text-center">
				<div class="damage" v-for="key in Object.keys(damage)">
					<b>{{key}}</b><span>{{(100 * damage[key]).toFixed()}}%</span>
				</div>
			</div>-->
    </div>
    <!--<div><b>Brand:</b><span>{{brand.name || brand.id}}</span></div>
		<div><b>Model:</b><span>{{telemetry.trailer.model.name || telemetry.trailer.model.id}}</span></div>
		<div><b>Accessory ID:</b><span>{{accessoryId}}</span></div>
		<div><b>Body type:</b><span>{{bodyType}}</span></div>
		<div><b>Chain type:</b><span>{{chainType}}</span></div>
		<div><b>License plate:</b><span>{{telemetry.trailer.licensePlate.value}} ({{telemetry.trailer.licensePlate.country.name}})</span></div>
		<div><b>Attached:</b><span>{{attached ? 'YES' : 'NO'}}</span></div>-->
  </div>
</template>

<script>
import TelemetryMixin from '@/mixins/TelemetryMixin';

export default {
  name: 'JagfxTrailer',
  mixins: [TelemetryMixin]
};
</script>
