<script>
  async function createCharacterObject() {
    const res = await fetch(
      'https://aceship.github.io/AN-EN-Tags/json/gamedata/en/excel/handbook_info_table.json'
    )
    const data = await res.json()
    const handbook = data.handbookDict

    let characters = []
    for (let char in handbook) {
      if (handbook[char].charID.startsWith('char_')) {
        characters.push({
          name: parseName(
            handbook[char].storyTextAudio[0].stories[0].storyText
          ),
          birthdate: parseBirthdate(
            handbook[char].storyTextAudio[0].stories[0].storyText
          ),
          image:
            'https://aceship.github.io/AN-EN-Tags/img/characters/' +
            handbook[char].charID +
            '_1.png',
          avatar:
            'https://aceship.github.io/AN-EN-Tags/img/avatars/' +
            handbook[char].charID +
            '_1.png',
        })
      }
    }

    return characters
  }

  function parseName(desc) {
    return desc
      .split('[Code Name] ')
      .pop()
      .split('\n')[0]
  }

  function parseBirthdate(desc) {
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

    return { month: month, day: parseInt(rawDate.match(/\d+/), 10) }
  }

  createCharacterObject().then(chars => {
    console.log(chars)
  })
</script>

<main>
  <div>test</div>
</main>
