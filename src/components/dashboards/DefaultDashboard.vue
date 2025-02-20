<template>
  <Dashboard v-slot="dashProps" class="default wrapper">
    <div
      class="dashboard game-connected yes"
      :style="{
        transform:
          'scale(' + dashProps.currentScale + ') translate(-50%, -50%)',
        width: dashProps.skinData.size.width + 'px',
        height: dashProps.skinData.size.height + 'px'
      }"
    >
      <div :class="{ yes: telemetry.job.cargo.id }" class="hasJob">
        <!-- meters -->
        <!--
          Attributes:
          data-min-angle: angle in degress for the arrow for data-min value (0 = vertical, negative = left, positive = right)
          data-max-angle: an gle in degress for the arrow for data-max value (0 = vertical, negative = left, positive = right)
          data-min: minimal possible value (as in JSON response), you may also use any telemetry property name for dynamic values
          data-max: maximum possible value (as in JSON response), you may also use any telemetry property name for dynamic values
          -->
        <Cadran
          v-bind="{
            classCSS: 'truck-speed',
            type: 'meter',
            value: telemetry.truck.speed.kph,
            min: 0,
            max: 140,
            minAngle: -114,
            maxAngle: 114
          }"
        />
        <div class="truck-speedRounded wrapper-area">
          <span>{{
            unit_speed(telemetry.truck.speed, true, false) | $toFixed(0)
          }}</span>
        </div>
        <div class="truck-speedRounded-unit wrapper-area">
          <span>{{ unit_speed(telemetry.truck.speed, false) }}</span>
        </div>
        <Cadran
          v-bind="{
            classCSS: 'truck-engineRpm',
            type: 'meter',
            value: telemetry.truck.engine.rpm.value / 100,
            min: 0,
            max: 24,
            minAngle: -97,
            maxAngle: 97
          }"
        />
        <Cadran
          v-bind="{
            classCSS: 'truck-fuel',
            type: 'meter',
            value: telemetry.truck.fuel.value,
            min: 0,
            max: telemetry.truck.fuel.capacity,
            minAngle: -96,
            maxAngle: 0
          }"
        />
        <Cadran
          v-bind="{
            classCSS: 'truck-waterTemperature',
            type: 'meter',
            value: telemetry.truck.engine.waterTemperature.value,
            min: 0,
            max: 100,
            minAngle: -96,
            maxAngle: 0
          }"
        />
        <div class="truck-odometer wrapper-area">
          <span>{{
            unit_length(telemetry.truck.odometer, 'km', true, false)
              | $toFixed(0)
          }}</span>
        </div>
        <div class="truck-cruiseControlSpeedRounded wrapper-area">
          <span>{{ telemetry.truck.cruiseControl.kph }}</span>
        </div>
        <div class="truck-gear wrapper-area">
          <span>{{
            $trukGear(telemetry.truck.transmission, telemetry.truck.brand)
          }}</span>
        </div>
        <!-- indicators -->
        <div
          :class="{ yes: telemetry.truck.lights.blinker.left.active }"
          class="truck-blinkerLeftOn"
        />
        <div
          :class="{ yes: telemetry.truck.lights.blinker.right.active }"
          class="truck-blinkerRightOn"
        />
        <div
          :class="{ yes: telemetry.truck.cruiseControl.enabled }"
          class="truck-cruiseControlOn"
        />
        <div
          :class="{ yes: telemetry.truck.lights.beamHigh.enabled }"
          class="truck-lightsBeamHighOn"
        />
        <div
          :class="{ yes: telemetry.truck.lights.beamLow.enabled }"
          class="truck-lightsBeamLowOn"
        />
        <div
          :class="{ yes: telemetry.truck.lights.parking.enabled }"
          class="truck-lightsParkingOn"
        />
        <div
          :class="{ yes: telemetry.trailer.attached }"
          class="trailer-attached"
        />
        <div class="trailer-mass">
          {{ unit_weight(telemetry.job.cargo.mass, true, false) | $toFixed(1)
          }}<span class="ton">{{
            unit_weight(telemetry.job.cargo.mass, false)
          }}</span>
        </div>
        <div class="trailer-name">
          {{ telemetry.job.cargo.name }}
        </div>
        <!-- job information -->
        <table class="_job">
          <tr>
            <th>{{ $t('Time') }}:</th>
            <td>
              <span class="game-time">{{
                $gameTime()
                  | $dateTimeLocalized(DATE_FORMAT_LONG, TIME_FORMAT_SHORT)
              }}</span>
            </td>
          </tr>
          <tr>
            <th>{{ $t('Source') }}:</th>
            <td>
              <span class="hasJob _jobSource">
                <span class="job-sourceCity">{{
                  telemetry.job.source.city.name
                }}</span>
                (<span class="job-sourceCompany">{{
                  telemetry.job.source.company.name
                }}</span
                >)
              </span>
            </td>
          </tr>
          <tr>
            <th>{{ $t('Destination') }}:</th>
            <td>
              <span class="hasJob _jobDestionation">
                <span class="job-destinationCity">{{
                  telemetry.job.destination.city.name
                }}</span>
                (<span class="job-destinationCompany">{{
                  telemetry.job.destination.company.name
                }}</span
                >)
              </span>
            </td>
          </tr>
          <tr>
            <th>{{ $t('Deadline in') }}:</th>
            <td>
              <span class="job-remainingTime">{{
                $jobRemainingTimeDelivery(
                  telemetry.job.expectedDeliveryTimestamp.value
                )
              }}</span>
              <span class="_jobIncome">
                (<span class="job-income">{{
                  unit_currency(telemetry.job.income)
                }}</span
                >)</span
              >
            </td>
          </tr>
        </table>
        <div class="d-flex">
          <div class="_truckWearInfo">
            {{ $t('Truck wear') }}:<br />
            <span class="truck-wearSum"
              >{{ $averageDamage(telemetry.truck.damage) }}%</span
            >
          </div>
          <div class="_trailerWearInfo">
            {{ $t('Trailer damage') }}:<br />
            <span class="trailer-wear"
              >{{ telemetry.trailer.chassis.damage.toFixed(0) }}%</span
            >
          </div>
        </div>
      </div>
    </div>
  </Dashboard>
</template>

<script>
import Dashboard from '@/components/dashboards/Dashboard';
import Cadran from '@/components/dashboards/shared/Cadran';
import TelemetryMixin from '@/mixins/TelemetryMixin';

export default {
  name: 'DafXFDashboard',
  components: {
    Dashboard,
    Cadran
  },
  mixins: [TelemetryMixin]
};
</script>
