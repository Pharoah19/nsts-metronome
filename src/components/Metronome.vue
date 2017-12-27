<template>
<div class="page">
  <display/>

  <time-signatures :time-signatures='[]'/>

  <div class='buttons-container'>
    <div v-on:click='toggleMetronomeOn' :class='toggleButtonCSS'>
      <metronome-svg />
      <p class='text'>{{ toggleButtonText }}</p>
    </div>

    <p class='button edit-button' v-if='false'>
      EDIT
    </p>
  </div>
</div>
</template>

<script>
import Display from './Display';
import TimeSignatures from './TimeSignatures';
import MetronomeSVG from './MetronomeSVG';

export default {
  components: {
    Display,
    TimeSignatures,
    'metronome-svg': MetronomeSVG
  },
  computed: {
    metronomeOn() {
      return this.$store.state.metronomeOn;
    },
    toggleButtonText() {
      return this.$store.state.metronomeOn ? 'STOP' : 'START';
    },
    toggleButtonCSS() {
      const modifier = this.$store.state.metronomeOn ? 'stop' : 'start';
      return `button toggle-metronome-button ${modifier}`;
    }
  },
  methods: {
    toggleMetronomeOn() {
      this.$store.dispatch({
        type: 'toggleMetronome',
      })
    },
  }
};
</script>

<style lang="scss" scoped>
@import '../style/_colors.scss';

.page {
  padding: 100px 20px 0;
  background-color: $background-black;
  height: 100%;
  text-align: center;
}

.change-bpm-modal {
  .modal-inner {
    background-color: $purple;
  }
}

.buttons-container {
  display: flex;
  max-width: 300px;
  margin: auto;
  justify-content: center;

  .button {
    padding: 10px 15px;
  }

  .toggle-metronome-button {
    font-size: 40px;
    padding: 12px 19px;
  }

  .toggle-metronome-button.start {
    background-color: $green;
    color: white;

    &:hover {
      background-color: $green-hover;
    }
  }

  .toggle-metronome-button {
    display: flex;
    align-items: center;

    .text {
      margin-left: 8px;
    }
  }

  .toggle-metronome-button.stop {
    background-color: $red;
    color: white;

    &:hover {
      background-color: $red-hover;
    }
  }

  .edit-button {
    background-color: $purple;
    color: white;

    &:hover {
      background-color: $purple-hover;
    }
  }
}
</style>