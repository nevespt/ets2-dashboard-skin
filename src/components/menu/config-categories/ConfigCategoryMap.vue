<template>
  <div>
    <div class="fields mb-4">
      <div class="mb-4">
        <h4>{{ $t('General') }}</h4>
        <ConfigFieldChoice
          v-bind="{
            id: 'maps_general_debug',
            label: 'Debug information',
            disabled: false,
            description: 'Display some debug information about the map',
            values: fieldValues('on_off'),
            target: 'game'
          }"
        />
      </div>

      <div class="mb-4">
        <h4>{{ $t('Elements') }}</h4>

        <ConfigFieldChoice
          v-bind="{
            id: 'maps_elements_eta',
            label: 'ETA information',
            disabled: false,
            description:
              'Display the remaining or ETA time and the current remaining distance to the destination',
            values: fieldValues('on_off'),
            target: 'game'
          }"
        />
        <ConfigFieldChoice
          v-bind="{
            id: 'maps_elements_speedAndGear',
            label: 'Speed and gear',
            disabled: false,
            description: 'Display the current speed and gear',
            values: fieldValues('on_off'),
            target: 'game'
          }"
        />
        <ConfigFieldChoice
          v-bind="{
            id: 'maps_elements_mapControls',
            label: 'Map controls',
            disabled: false,
            description:
              'Display map controls (Recenter, focus on user, zoom in and zoom out)',
            values: fieldValues('on_off'),
            target: 'game'
          }"
        />
        <ConfigFieldChoice
          v-bind="{
            id: 'maps_elements_speedLimit',
            label: 'Speed limit',
            disabled: false,
            description: 'Display current speed limit',
            values: fieldValues('on_off'),
            target: 'game'
          }"
        />
        <ConfigFieldChoice
          v-bind="{
            id: 'maps_elements_rotateWithPlayer',
            label: 'Map rotation',
            disabled: !configEnabled('maps_elements_mapControls'),
            description: 'Enable or disable the map rotation on the first load',
            values: fieldValues('on_off'),
            target: 'game'
          }"
        />
        <ConfigFieldChoice
          v-bind="{
            id: 'maps_map_navigationRemaining',
            label: 'Navigation ETA',
            disabled: !configEnabled('maps_elements_eta'),
            description:
              'Display the due date or the remaining time for the current route',
            values: fieldValues('maps_map_navigationRemaining'),
            target: 'game'
          }"
        />
      </div>
    </div>
    <div class="fields mb-4">
      <h4>{{ $t('Tiles') }}</h4>

      <ConfigFieldChoice
        v-bind="{
          id: 'maps_map_activeMap',
          label: 'Active map',
          disabled: false,
          description: 'Change the active map',
          values: fieldValues('maps_map_activeMap'),
          target: 'game'
        }"
      />
      <ConfigFieldChoice
        v-bind="{
          id: 'maps_map_type',
          label: 'Kind of map',
          disabled: false,
          description:
            'Use the ETS2 or ATS map automatically or use the modded map',
          values: fieldValues('maps_map_type'),
          target: 'game'
        }"
      />
      <ConfigFieldChoice
        v-bind="{
          id: 'maps_map_tilesRemotePath',
          label: 'Remote tiles location',
          disabled: configEnabled('maps_map_tilesRemoteUseCustom'),
          description: 'Set a remote location for the map tiles.',
          values: fieldValues('maps_map_tilesRemotePath'),
          target: 'game'
        }"
      />
      <ConfigFieldChoice
        v-bind="{
          id: 'maps_map_tilesRemoteUseCustom',
          label: 'Custom tiles',
          disabled: false,
          description: 'Set to ON if you wan to use a custom tiles location',
          values: fieldValues('on_off'),
          target: 'game'
        }"
      />
      <ConfigFieldInput
        v-bind="{
          id: 'maps_map_tilesRemoteCustomPath',
          label: 'Custom tiles location',
          disabled: !configEnabled('maps_map_tilesRemoteUseCustom'),
          description: 'The host of your tiles location',
          target: 'game'
        }"
      />
      <ConfigFieldChoice
        v-bind="{
          id: 'maps_map_tilesVersion',
          label: 'Game version',
          disabled: configEnabled('maps_map_tilesRemoteUseCustom'),
          description:
            'Get tiles for the latest game version, or for the specified game version',
          values: fieldValues('maps_map_tilesVersion'),
          target: 'game'
        }"
      />
    </div>
  </div>
</template>

<script>
import ConfigCategoryMixin from '@/mixins/ConfigCategoryMixin';

export default {
  name: 'ConfigCategoryMap',
  mixins: [ConfigCategoryMixin]
};
</script>
