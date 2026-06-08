<script lang="ts" setup>
import { ref, onMounted, onUnmounted } from 'vue'

const codeSnippets = [
  { // Playwright — the conversion
    code: `import { test, expect } from '@playwright/test';\n\ntest('jonathan: developer becomes QA engineer', async ({ page }) => {\n  await page.goto('/career');\n\n  await expect(page.getByTestId('role'))\n    .toHaveText('Web Developer');\n\n  await page.getByRole('button', { name: 'Change career' }).click();\n\n  await expect(page.getByTestId('role'))\n    .toHaveText('QA Engineer');\n});`
  },
  { // Drupal hook — the career pivot
    code: `<?php\n/**\n * Implements hook_user_role_alter().\n *\n * Transitions a web developer into a QA engineer.\n */\nfunction career_hook_user_role_alter(array &$roles, AccountInterface $account) {\n  if (in_array('web_developer', $roles)) {\n    unset($roles['web_developer']);\n    $roles['qa_engineer'] = TRUE;\n    $account->set('perspective', 'I know where bugs are born');\n  }\n}`
  },
  { // GitHub Actions CI
    code: `# .github/workflows/qa.yml\nname: QA Pipeline\n\non: [pull_request]\n\njobs:\n  test:\n    runs-on: ubuntu-latest\n    steps:\n      - uses: actions/checkout@v4\n      - uses: actions/setup-node@v4\n      - run: npm ci\n      - run: npx playwright install --with-deps\n      - run: npm run test:e2e`
  },
]

const displayText = ref('')

let snippetIndex = 0
let charIndex = 0
let isDeleting = false
let timeoutId: ReturnType<typeof setTimeout> | null = null

const TYPING_SPEED = 20      // ms per character when typing
const DELETING_SPEED = 5    // ms per character when erasing
const PAUSE_DURATION = 2500  // How long to display completed code

function handleTyping() {
  const currentSnippet = codeSnippets[snippetIndex]
  if(!currentSnippet) {
    return;
  }
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
  min-height: 400px;
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