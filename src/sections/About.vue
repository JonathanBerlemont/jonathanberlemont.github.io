<script lang="ts" setup>
import Greeblies from '@/components/Greeblies.vue';
import socials from '@/data/socials.json';
</script>

<template>
<h1 class="ascii-container">
    <div class="ascii-line first">
        <pre class="ascii-text">
       _                   _   _         
      | |                 | | | |        
      | | ___  _ __   __ _| |_| |__   __ _ _ __  
  _   | |/ _ \| '_ \ / _` | __| '_ \ / _` | '_ \ 
 | |__| | (_) | | | | (_| | |_| | | | (_| | | | |
  \____/ \___/|_| |_|\__,_|\__|_| |_|\__,_|_| |_|
        </pre>
    </div>
    <div class="ascii-line last">
        <pre class="ascii-text">
  ____            _                            _   
 |  _ \          | |                          | |  
 | |_) | ___ _ __| | ___ _ __ ___   ___  _ __ | |_ 
 |  _ < / _ \ '__| |/ _ \ '_ ` _ \ / _ \| '_ \| __|
 | |_) |  __/ |  | |  __/ | | | | | (_) | | | | |_ 
 |____/ \___|_|  |_|\___|_| |_| |_|\___/|_| |_|\__|
        </pre>
    </div>
</h1>
    <v-card variant="outlined" class="about-card">
        <div class="about">
            <p>I have over 6 years of experience building web applications, starting at Deloitte where I worked on LMS platforms, followed by 5 years at Sciensano developing healthcare software within a small team and contributing to increasingly complex systems.</p>
            <p>It was at Sciensano that I developed a real interest in quality engineering: as the amount of projects grew and their infrastructures became more and more complex, the need for proper monitoring and structured testing became increasingly apparent. I found myself more interested in solving those challenges than in feature development itself.</p>
            <p>My background as a developer gives me a perspective that many non-technical testers do not have. I understand how defects are introduced, where they are likely to occur, and how developers approach debugging. This allows me to collaborate effectively with development teams and provide the detailed, actionable information I know they need to resolve issues efficiently.</p>
            <div class="socials d-flex flex-wrap ga-3">
                <v-chip 
                    v-for="social in socials"
                    :key="social.name"
                    :href="social.url"
                    :prepend-icon="social.icon"
                    color="#00ff66"
                    target="_blank"
                >
                {{ social.title }}
                </v-chip>
            </div>
        </div>
        <div class="greeblies d-none d-md-block">
            <Greeblies />
        </div>
    </v-card>
</template>

<style scoped>
.ascii-container {
    align-items: center;
}

@media (max-width: 768px) {
    .ascii-container {
        flex-direction: column;
    }

    .ascii-line.first {
        transform: translateX(-15%);
    }

    .ascii-line.last {
        transform: translateX(15%);
    }
}
.about-card {
    display: grid;
    grid-template-columns: 2fr 1fr; 
    gap: 20px; 
    padding: 20px;
    .about {
        display: flex;
        flex-direction: column;
        height: 100%;
        .socials {
            margin-top: auto;
            .v-chip {
                transition: transform 0.2s ease;
                &:hover {
                    transform: scale(1.1);
                }
            }
        }
    }
}
@media (max-width: 768px) {
    .about-card {
        grid-template-columns: 1fr;
    }
}
</style>
