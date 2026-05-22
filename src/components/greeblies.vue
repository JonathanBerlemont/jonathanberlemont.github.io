<script lang="ts" setup>
import { ref, onMounted, onUnmounted } from 'vue'

// Real, structural code snippets to cycle through
const codeSnippets = [
  { // Playwright 
    code: `import { test, expect } from '@playwright/test';\n\ndescribe('QA Automation Pipeline', () => {\n  test('should pass regression form submission', async ({ page }) => {\n    await page.goto('/contact');\n    await page.getByLabel('Full Name').fill('QA Engineer');\n    await page.getByRole('button', { name: 'Submit' }).click();\n    \n    await expect(page.getByTestId('success-alert')).toBeVisible();\n  });\n});`
  },
  { // Drupal 10/11
    code: `<?php\nnamespace Drupal\\qa_insights\\Controller;\n\nuse Drupal\\Core\\Controller\\ControllerBase;\nuse Symfony\\Component\\HttpFoundation\\JsonResponse;\n\nclass AuditReportController extends ControllerBase {\n  public function getLatestMetrics(): JsonResponse {\n    $data = ['status' => 'optimized', 'coverage' => 94.2];\n    return new JsonResponse($data);\n  }\n}`
  },
  { // Vue 3.5 
    code: `import { ref, computed, watchEffect } from 'vue';\n\nconst totalErrors = ref(0);\nconst systemStatus = computed(() => \n  totalErrors.value === 0 ? 'Healthy' : 'Degraded'\n);\n\nwatchEffect(() => {\n  if (totalErrors.value > 5) alertCriticalTelemetry();\n});`
  },
]

const displayText = ref('')

let snippetIndex = 0
let charIndex = 0
let isDeleting = false
let timeoutId: ReturnType<typeof setTimeout> | null = null

const TYPING_SPEED = 40      // ms per character when typing
const DELETING_SPEED = 10    // ms per character when erasing
const PAUSE_DURATION = 2500  // How long to display completed code

function handleTyping() {
  const currentSnippet = codeSnippets[snippetIndex]
  const fullText = currentSnippet.code

  if (!isDeleting) {
    // Typing forward
    displayText.value = fullText.slice(0, charIndex + 1)
    charIndex++

    if (charIndex === fullText.length) {
      // Pause when full snippet is typed out
      timeoutId = setTimeout(() => {
        isDeleting = true
        handleTyping()
      }, PAUSE_DURATION)
      return
    }
  } else {
    // Erasing backward
    displayText.value = fullText.slice(0, charIndex - 1)
    charIndex--

    if (charIndex === 0) {
      isDeleting = false
      // Move to the next snippet, loop back to start if at the end
      snippetIndex = (snippetIndex + 1) % codeSnippets.length
    }
  }

  // Set the speed dynamically based on typing or deleting action
  const nextSpeed = isDeleting ? DELETING_SPEED : TYPING_SPEED
  timeoutId = setTimeout(handleTyping, nextSpeed)
}

onMounted(() => {
  handleTyping()
})

onUnmounted(() => {
  if (timeoutId) clearTimeout(timeoutId)
})
</script>

<template>
  <div class="code-greeblie-container">
    <!-- Code Box -->
    <pre><code>{{ displayText }}<span class="blinking-cursor">|</span></code></pre>
  </div>
</template>

<style scoped>
.code-greeblie-container {
  background-color: #1e1e1e;
  border-radius: 6px;
  padding: 16px;
  font-family: 'Fira Code', 'Courier New', Courier, monospace;
  font-size: 0.85rem;
  line-height: 1.5;
  height: 100%;
  height: 350px;
  display: flex;
  flex-direction: column;
  position: relative;
  overflow: hidden;
  box-shadow: inset 0 0 10px rgba(0, 0, 0, 0.5);
}

pre {
  margin: 0;
  white-space: pre-wrap;
  word-wrap: break-word;
  color: #00ff66;
  text-shadow: 0 0 8px rgba(0, 255, 102, 0.65);
}
.blinking-cursor {
  color: #00ff66;
  font-weight: bold;
  animation: blink 1s step-end infinite;
}

@keyframes blink {
  from, to { opacity: 1 }
  50% { opacity: 0 }
}
</style>