<script lang="ts">
  let exception = ""
  let output = ""

  function simplifyException(text: string): string {
    return text
      .split("\n")
      .map((line) => {
        var rgx = /at (.+)(<.*>.*)?(\(.*\))( in )?(.+)?/
        var match = rgx.exec(line)
        if (match) {
          var fullyQualifiedName = match[1] || ""
          var fullFilePath = match[5] || ""

          var methodName = fullyQualifiedName.split(".").at(-1)
          var fileName = fullFilePath.split("/").at(-1)

          var fileReference = fileName ? ` in ${fileName}` : ""
          var truncatedLine = `at ${methodName}()${fileReference}`

          return truncatedLine
        }
        return line.trim()
      })
      .join("\n")
  }

  function transform() {
    output = simplifyException(exception)
  }
</script>

<main>
  <h1>Exception Simplifier</h1>
  <textarea bind:value={exception} placeholder="Paste your exception here"></textarea>
  <br />
  <button on:click={transform}>Transform</button>
  <pre>{output}</pre>
</main>

<style>
  textarea {
    width: 100%;
    height: 200px;
    margin-bottom: 1rem;
    font-family: monospace;
    font-size: 0.9rem;
  }

  button {
    margin-bottom: 1rem;
  }

  pre {
    background: #f9f9f9;
    padding: 1rem;
    border: 1px solid #ddd;
    font-family: monospace;
    white-space: pre-wrap;
  }
</style>
