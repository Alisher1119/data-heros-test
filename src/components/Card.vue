<template>
  <div class="card">
    <div class="card-img">
      <img :src="item.image">
    </div>
    <div class="card-caption">
      <div class="section">
        <h2>{{item.name}}</h2><span class="status"><span :class="'status__icon ' + item.status"></span> {{ item.status }} - {{item.species}}</span>
      </div>
      <div class="section">
        <span class="text-gray">Last known location:</span>
        <div>
          <span class="text-18">{{ item.location.name }}</span>
        </div>
      </div>
      <div class="section">
        <span class="text-gray">First seen in:</span>
        <div>
          <span class="text-18">{{ item.origin.name }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import type {CharacterInterface} from "@/interfaces/character.interface";

interface CardProps {
  item: CharacterInterface;
}

const props = defineProps<CardProps>();

</script>

<style lang="scss" scoped>
.card {
  width: 600px;
  height: 220px;
  display: flex;
  overflow: hidden;
  background: rgb(60, 62, 68);
  border-radius: 0.5rem;
  margin: 0.75rem;
  box-shadow: rgba(0, 0, 0, 0.1) 0px 4px 6px -1px, rgba(0, 0, 0, 0.06) 0px 2px 4px -1px;

  &-img {
    flex: 2 1 0;
    width: 100%;

    img {
      width: 100%;
      height: 100%;
      margin: 0;
      opacity: 1;
      transition: opacity 0.5s ease 0s;
      object-position: center center;
      object-fit: cover;
    }
  }

  &-caption {
    flex: 3 1 0;
    position: relative;
    padding: 0.75rem;
    color: rgb(255, 255, 255);
    display: flex;
    flex-direction: column;
    justify-content: flex-start;

    .section {
      flex: 1 1 0;
      display: flex;
      flex-direction: column;
      justify-content: center;

      &:first-child {
        justify-content: flex-start;
      }

      h2 {
        font-size: 27px;
        margin: 0;
        padding: 0;
        font-weight: 900;
      }
    }

    .status {
      display: flex;
      align-items: center;
      text-transform: capitalize;

      &__icon {
        height: 0.5rem;
        width: 0.5rem;
        margin-right: 0.375rem;
        border-radius: 50%;

        &.Alive {
          background: rgb(85, 204, 68);
        }

        &.Dead {
          background: rgb(214, 61, 46);
        }
        &.unknown {
          background: rgb(214, 161, 46);
        }
      }
    }
  }
}


</style>
