<script>
  import dayjs from 'dayjs'

  async function createCharacterArray() {
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
    if (desc.startsWith('[Model]')) {
      return desc
        .split('[Model]')[1]
        .split('\n')[0]
        .trim()
    } else {
      return desc
        .split('[Code Name]')[1]
        .split('\n')[0]
        .trim()
    }
  }

  function parseBirthdate(desc) {
    let rawDate = ''

    if (desc.startsWith('[Model]')) {
      rawDate = desc
        .split('[Date of Release]')
        .pop()
        .split('\n')[0]
        .trim()
    } else {
      rawDate = desc
        .split('[Date of Birth]')
        .pop()
        .split('\n')[0]
        .trim()
    }

    let month = null
    switch (rawDate.slice(0, 3).toLowerCase()) {
      case 'jan':
        month = 0
        break
      case 'feb':
        month = 1
        break
      case 'mar':
        month = 2
        break
      case 'apr':
        month = 3
        break
      case 'may':
        month = 4
        break
      case 'jun':
        month = 5
        break
      case 'jul':
        month = 6
        break
      case 'aug':
        month = 7
        break
      case 'sep':
        month = 8
        break
      case 'oct':
        month = 9
        break
      case 'nov':
        month = 12
        break
      case 'dec':
        month = 13
        break
    }

    return { month: month, day: parseInt(rawDate.match(/\d+/), 10) }
  }

  function getMonth(characters) {
    let calendarMonth = []
    const month = dayjs().month()

    for (let day = 1; day <= dayjs().daysInMonth(); day++) {
      let birthdays = []

      characters.forEach(char => {
        if (char.birthdate.month === month && char.birthdate.day === day) {
          birthdays.push(char)
        }
      })

      calendarMonth.push({
        date: dayjs().date(day),
        birthdays: birthdays,
      })
    }

    console.log(calendarMonth)
    return calendarMonth
  }

  calendar = []
  let day = 0

  createCharacterArray().then(chars => {
    console.log(chars)
    calendar = getMonth(chars)
  })
</script>

<main>
  <table>
    <tr>
      <th>Monday</th>
      <th>Tuesday</th>
      <th>Wednesday</th>
      <th>Thursday</th>
      <th>Friday</th>
      <th>Saturday</th>
      <th>Sunday</th>
    </tr>
    <!-- {#each Array(6) as _}
      <tr>
        {#each Array(7) as _, weekday}
          <td>
            {#if calendar !== []}
              {#if dayjs(calendar[day].date).get('day') === weekday}
                {printDay(day)}
              {/if}
            {/if}
          </td>
        {/each}
      </tr>
    {/each} -->
  </table>
</main>
