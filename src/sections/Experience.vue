<script lang="ts" setup>
import TagList from "@/components/TagList.vue";
import experiences from "@/data/experiences.json";

const MONTHS: Record<string, number> = {
  "January":0, 
  "February":1, 
  "March":2, 
  "April":3, 
  "May":4, 
  "June":5,
  "July":6, 
  "August":7, 
  "September":8, 
  "October":9, 
  "November":10, 
  "December":11
};

function calcDuration(start: string, end: string) {
  const parseDate = (str:string) => {
    if (str === "Now") return new Date();
    const [month, year] = str.split(" ");
    if(!month || !year) {
        return new Date();
    }
    return new Date(parseInt(year), MONTHS[month] ?? 0, 1);
  };
  const s = parseDate(start);
  const e = parseDate(end);
  let months = (e.getFullYear() - s.getFullYear()) * 12 + (e.getMonth() - s.getMonth());
  const years = Math.floor(months / 12);
  const rem = months % 12;
  let parts = [];
  if (years > 0) parts.push(years + (years === 1 ? " year" : " years"));
  if (rem > 0) parts.push(rem + " months");
  return parts.join(" ") || "< 1 months";
}
</script>

<template>
    <h2 class="ascii-container" title="Experience">
        <span class="d-sr-only">Experience</span>
        <pre class="ascii-text" aria-hidden="true">
  ______                      _                     
 |  ____|                    (_)                    
 | |__  __  ___ __   ___ _ __ _  ___ _ __   ___ ___ 
 |  __| \ \/ / '_ \ / _ \ '__| |/ _ \ '_ \ / __/ _ \
 | |____ >  <| |_) |  __/ |  | |  __/ | | | (_|  __/
 |______/_/\_\ .__/ \___|_|  |_|\___|_| |_|\___\___|
             | |                                    
             |_|                                    
        </pre>
    </h2>

    <div class="experiences">
        <v-card
            v-for="experience in experiences"
            :key="experience.title"
            color="#00ff66"
            variant="outlined"
            class="mb-5"
        >
            <template #append>
                <div class="company-logo" style="border: 1px solid currentColor; border-radius: 5px; padding: 8px 12px; background-color: color-mix(in srgb, currentColor 15%, transparent);">
                    <img :src="`/logos/${experience.logo}`" style="width: 120px; object-fit: contain;" />
                </div>
            </template>

            <template #title>
                {{ experience.title }}
            </template>

            <template #subtitle>
                {{ experience.company }} · {{ experience.started }} – {{ experience.finished }}
                <v-chip size="small" variant="outlined" class="ml-2">
                    {{ calcDuration(experience.started, experience.finished) }}
                </v-chip>
            </template>

            <v-card-text>
                <p class="mb-3">{{ experience.description }}</p>

                <ul class="bullets mb-3">
                    <li v-for="bullet in experience.bullets" :key="bullet">
                        {{ bullet }}
                    </li>
                </ul>
                
                <v-dialog max-width="800" v-if="experience.highlights">
                    <template #activator="{ props }">
                        <v-btn color="#00ff66" variant="outlined" class="mb-3" v-bind="props" append-icon="mdi-creation">
                            Projects Highlights
                        </v-btn>
                    </template>

                    <v-card color="#00ff66" variant="outlined" class="highlight-card">
                        <template #title>
                            {{ experience.company }} — Highlights
                        </template>
                        <v-card-text>
                            <ul>
                                <li
                                    v-for="highlight in experience.highlights" 
                                    :key="highlight.url"
                                    class="mb-5"
                                >
                                    <v-btn
                                        :href="highlight.url"
                                        target="_blank"
                                        rel="noopener noreferrer"
                                        variant="outlined"
                                        color="#00ff66"
                                        append-icon="mdi-open-in-new"
                                    >
                                        {{ highlight.url }}
                                    </v-btn>
                                    <p>{{ highlight.description }}</p>
                                </li>
                            </ul>
                            
                        </v-card-text>
                    </v-card>
                </v-dialog>

                <TagList :tags="experience.tags" />

            </v-card-text>
        </v-card>
    </div>

</template>

<style scoped>
@media (max-width: 768px) {
    .v-card .company-logo {
        display: none;
    }
}
p, ul {
    color: white;
}
.highlight-card {
    background-color: black;
    ul {
        list-style: none;
        padding-left: 0;

        li:not(:last-child) { border-bottom: solid 1px #006633; }
    }
}
</style>