<template>
  <v-container>
    <h1>Convert YAML/TOML</h1>
    <v-row>
      <v-col>
        <v-textarea
          outlined
          label="YAML"
          height="90%"
          :value="yaml"
          :error-messages="yamlError"
          @input="onYamlChanged"
        >
        </v-textarea>
      </v-col>
      <v-col>
        <v-textarea
          outlined
          label="TOML"
          :value="toml"
          :error-messages="tomlError"
          @input="onTomlChanged"
        >
        </v-textarea>
      </v-col>
    </v-row>
  </v-container>
</template>

<script lang="ts">
import { Component, Vue, Watch } from 'vue-property-decorator'
import * as YAML from 'js-yaml'
import * as TOML from '@iarna/toml'

@Component
export default class IndexPage extends Vue {
  yaml = ''
  toml = ''
  yamlError = null
  tomlError = null

  onYamlChanged(value: string): void {
    try {
      this.yaml = value
      this.toml = TOML.stringify(YAML.safeLoad(value))
      this.yamlError = null
    } catch (e) {
      this.yamlError = e.toString()
    }
  }

  onTomlChanged(value: string): void {
    try {
      this.toml = value
      this.yaml = YAML.safeDump(TOML.parse(value))
      this.tomlError = null
    } catch (e) {
      this.tomlError = e.toString()
    }
  }
}
</script>
