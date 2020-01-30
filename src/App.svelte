<script>
  async function createCharacterObject() {
    const res = await fetch(
      'https://aceship.github.io/AN-EN-Tags/json/gamedata/en/excel/handbook_info_table.json'
    )
    let handbook = await res.json()
    handbook = handbook.handbookDict

    for (let char in handbook) {
      console.log('-')
      console.log(handbook[char].charID)
      console.log(handbook[char].storyTextAudio[0].stories[0].storyText)
    }
  }

  createCharacterObject()
</script>

<main>
  <div>test</div>
</main>
