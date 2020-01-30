<script>
  async function createCharacterObject() {
    const res = await fetch(
      'https://aceship.github.io/AN-EN-Tags/json/gamedata/en/excel/handbook_info_table.json'
    )
    const data = await res.json()
    const handbook = data.handbookDict

    console.log(handbook)

    for (let char in handbook) {
      if (handbook[char].charID.startsWith('char_')) {
        console.log('-')
        console.log(handbook[char].charID)
        console.log(
          parseBirthday(handbook[char].storyTextAudio[0].stories[0].storyText)
        )
      }
    }
  }

  function parseBirthday(desc) {
    let rawDate = desc
      .split('[Date of Birth] ')
      .pop()
      .split('\n')[0]

    let month = 0
    switch (rawDate.slice(0, 3)) {
      case 'Jan':
        month = 1
        break
      case 'Feb':
        month = 2
        break
      case 'Mar':
        month = 3
        break
      case 'Apr':
        month = 4
        break
      case 'May':
        month = 5
        break
      case 'Jun':
        month = 6
        break
      case 'Jul':
        month = 7
        break
      case 'Aug':
        month = 8
        break
      case 'Sep':
        month = 9
        break
      case 'Oct':
        month = 10
        break
      case 'Nov':
        month = 11
        break
      case 'Dec':
        month = 12
        break
    }

    return ' Month: ' + month + ' Day: ' + parseInt(rawDate.match(/\d+/), 10)
  }

  createCharacterObject()
</script>

<main>
  <div>test</div>
</main>
