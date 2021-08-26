<template>
  <div class="ctr">
    <transition name="fade" mode="out-in">
 <question
      v-if="questionsAnswered < questions.length"
      :questions="questions"
      :questionsAnswered="questionsAnswered"
      @question-answered="questionAnswered"
    ></question>
        <result v-else :results="results" :totalCorrect="totalCorrect"></result>
    </transition>
   <div class="right">Всего правильных ответов: {{totalCorrect}}</div>


    <button
      type="button"
      class="reset-btn"
      @click.prevent="reset"
      v-if="questionsAnswered === questions.length"
    >
      Reset
    </button>

  </div>
</template>

<script>
import Question from "./components/Question";
import Result from "./components/Result";
export default {
  name: "App",
  data() {
    return {
      questionsAnswered: 0,
      totalCorrect: 0,
      questions: [
        {
          q: "К какому году планировали построить коммунизм в СССР?",
          answers: [
            {
              text: "1970 году",
              is_correct: false,
            },
            {
              text: "2020 году",
              is_correct: false,
            },
            {
              text: "1980 году ",
              is_correct: true,
            },
            {
              text: "1930 году",
              is_correct: false,
            },
          ],
        },
        {
          q: "Как зовут мальчика из мультфильма 'Трое из Простоквашино'?",
          answers: [
            {
              text: "Серега",
              is_correct: false,
            },
            {
              text: "Мальчик Коля",
              is_correct: false,
            },
            {
              text: "Афонасий",
              is_correct: false,
            },
            {
              text: "Дядя Федор",
              is_correct: true,
            },
          ],
        },
        {
          q: "У какого животного кроме слона есть хобот?",
          answers: [
            {
              text: "Тапир",
              is_correct: true,
            },
            {
              text: "Утконос",
              is_correct: false,
            },
            {
              text: "Вилорог",
              is_correct: false,
            },
            {
              text: "Хобонос",
              is_correct: false,
            },
          ],
        },
        {
          q: "Что такое брюки клеш?",
          answers: [
            {
              text: "Очень узкие брюки",
              is_correct: false,
            },
            {
              text: "Длинные расширяющиеся к низу брюки",
              is_correct: true,
            },
            {
              text: "Легкие летние брюки",
              is_correct: false,
            },
            {
              text: "Штаны для ношения в плохую погоду",
              is_correct: false,
            },
          ],
        },
        {
          q: "Кто из президентов США написал свой собственный рассказ про Шерлока Холмса?",
          answers: [
            {
              text: "Джон Кеннеди",
              is_correct: false,
            },
            {
              text: "Франклин Рузвельт",
              is_correct: true,
            },
            {
              text: "Рональд Рейган",
              is_correct: false,
            },
            {
              text: "Барак Обама",
              is_correct: false,
            },
          ],
        },
        {
          q: "Какую пошлину ввели в XII  веке в Англии для того чтобы заставить мужчин пойти на войну?",
          answers: [
            {
              text: "Налог на тунеядство",
              is_correct: false,
            },
            {
              text: "Налог на отсутствие сапог",
              is_correct: false,
            },
            {
              text: "Налог на трусость",
              is_correct: true,
            },
            {
              text: "Повышенный налог на имущество",
              is_correct: false,
            },
          ],
        },
        {
          q: "Откуда пошло выражение «деньги не пахнут?",
          answers: [
            {
              text: "От подателей за провоз парфюмерии",
              is_correct: false,
            },
            {
              text: "От сборов за нестиранные носки",
              is_correct: false,
            },
            {
              text: "От налога на туалеты",
              is_correct: true,
            },
            {
              text: "От продавцов трупов для научных исследований",
              is_correct: false,
            },
          ],
        },
        {
          q: "Основой для «Сказки о рыбаке и рыбке Пушкина послужила сказка братьев Гримм «Рыбак и его жена». В ней немецкая «коллега» нашей старухи превратилась в:",
          answers: [
            {
              text: "Папу Римского",
              is_correct: true,
            },
            {
              text: "Королеву",
              is_correct: false,
            },
            {
              text: "Директора рыбзавода",
              is_correct: false,
            },
            {
              text: "Командира отряда водолазов ",
              is_correct: false,
            },
          ],
        },
        {
          q: "Российский мультфильм, удостоенный «Оскара», — это…",
          answers: [
            {
              text: "Простоквашино",
              is_correct: false,
            },
            {
              text: "Винни-Пух",
              is_correct: false,
            },
            {
              text: "Старик и море",
              is_correct: true,
            },
            {
              text: "Ну, погоди!",
              is_correct: false,
            },
          ],
        },
        {
          q: "Кто из знаменитых художников за жизнь продал всего одну картину? ",
          answers: [
            {
              text: "Пьер Огюст Ренуар",
              is_correct: false,
            },
            {
              text: "Каземир Малевич",
              is_correct: false,
            },
            {
              text: "Пабло Пикассо",
              is_correct: false,
            },
            {
              text: "Винсент Ван Гог",
              is_correct: true,
            },
          ],
        },
        {
          q: "У индейцев из немногочисленного североамериканского племени квакиутл есть традиция: беря деньги в долг, они оставляют в залог…",
          answers: [
            {
              text: "Душу",
              is_correct: false,
            },
            {
              text: "Имя",
              is_correct: true,
            },
            {
              text: "Скальп тещи",
              is_correct: false,
            },
            {
              text: "Амулет",
              is_correct: false,
            },
          ],
        },
        {
          q: "Как называют жителей города Смоленска в РФ?",
          answers: [
            {
              text: "Смоляне",
              is_correct: true,
            },
            {
              text: "Смоленяне",
              is_correct: false,
            },
            {
              text: "Мольки",
              is_correct: false,
            },
            {
              text: "Жители Смоленска",
              is_correct: false,
            },
          ],
        },
        {
          q: "Согласно пословице, до какой столицы может довести язык?",
          answers: [
            {
              text: "Монреаль",
              is_correct: false,
            },
            {
              text: "Нур-султан",
              is_correct: false,
            },
            {
              text: "Киев",
              is_correct: true,
            },
            {
              text: "Париж",
              is_correct: false,
            },
          ],
        },
        {
          q: "Назовите самое соленое море в Мировом океане",
          answers: [
            {
              text: "Мертвое море",
              is_correct: false,
            },
            {
              text: "Красное море",
              is_correct: true,
            },
            {
              text: "Черное море",
              is_correct: false,
            },
            {
              text: "Баренцево море",
              is_correct: false,
            },
          ],
        },
        {
          q: "Сколько в среднем весят мышцы человека?",
          answers: [
            {
              text: "40% от массы тела",
              is_correct: true,
            },
            {
              text: "20% от массы тела",
              is_correct: false,
            },
            {
              text: "54% от массы тела",
              is_correct: false,
            },
            {
              text: "16% от массы тела",
              is_correct: false,
            },
          ],
        },
        {
          q: "В каком году Титаник утонул в Атлантическом океане 15 апреля во время своего первого плавания из Саутгемптона?",
          answers: [
            {
              text: "1918",
              is_correct: false,
            },
            {
              text: "1900",
              is_correct: false,
            },
            {
              text: "1912",
              is_correct: true,
            },
            {
              text: "1875",
              is_correct: false,
            },
          ],
        },
        {
          q: "Как называется крупнейшая технологическая компания в Южной Корее?",
          answers: [
            {
              text: "Samsung",
              is_correct: true,
            },
            {
              text: "Huawei",
              is_correct: false,
            },
            {
              text: "Kioto-production",
              is_correct: true,
            },
            {
              text: "Toyota",
              is_correct: false,
            },
          ],
        },
        {
          q: "Столица Португалии?",
          answers: [
            {
              text: "Порту",
              is_correct: false,
            },
            {
              text: "Лиссабон",
              is_correct: true,
            },
            {
              text: "Алматы",
              is_correct: false,
            },
            {
              text: "Оттава",
              is_correct: false,
            },
          ],
        },
        {
          q: "Полное имя куклы Барби?",
          answers: [
            {
              text: "Барбара Брыльска",
              is_correct: false,
            },
            {
              text: "Сара Барбер",
              is_correct: false,
            },
            {
              text: "Джоди Барбериа",
              is_correct: false,
            },
            {
              text: "Барбара Миллисент Робертс",
              is_correct: true,
            },
          ],
        },
        {
          q: "За что держит рекорд Пол Ханн, который зарегистрировал 118.1 децибела?",
          answers: [
            {
              text: "Самый громкий пук",
              is_correct: false,
            },
            {
              text: "Самая громкая отрыжка",
              is_correct: true,
            },
            {
              text: "Самый громкий чих",
              is_correct: false,
            },
            {
              text: "Самый громкий храп",
              is_correct: false,
            },
          ],
        },
        {
          q: "Что было указано на визитной карточке Аль Капоне?",
          answers: [
            {
              text: "Продавец подержанной мебели",
              is_correct: true,
            },
            {
              text: "Убийца",
              is_correct: false,
            },
            {
              text: "Адвокат",
              is_correct: false,
            },
            {
              text: "Мед. брат",
              is_correct: false,
            },
          ],
        },
        {
          q: "Какова продолжительность жизни стрекозы?",
          answers: [
            {
              text: "7 дней",
              is_correct: false,
            },
            {
              text: "22 минуты",
              is_correct: false,
            },
            {
              text: "3 года",
              is_correct: false,
            },
            {
              text: "24 часа",
              is_correct: true,
            },
          ],
        },
        {
          q: "В каком году был выпущен Крестный отец?",
          answers: [
            {
              text: "1957",
              is_correct: false,
            },
            {
              text: "2000",
              is_correct: false,
            },
            {
              text: "1990",
              is_correct: false,
            },
            {
              text: "1972",
              is_correct: true,
            },
          ],
        },
        {
          q: "Сколько игроков в олимпийской команде по керлингу?",
          answers: [
            {
              text: "4",
              is_correct: true,
            },
            {
              text: "11",
              is_correct: false,
            },
            {
              text: "2",
              is_correct: false,
            },
            {
              text: "20",
              is_correct: false,
            },
          ],
        },
        {
          q: "В каком году «Битлз» впервые отправились в США?",
          answers: [
            {
              text: "1930",
              is_correct: false,
            },
            {
              text: "1944",
              is_correct: false,
            },
            {
              text: "1964",
              is_correct: true,
            },
            {
              text: "1980",
              is_correct: false,
            },
          ],
        },
        {
          q: "Где в мире выставлена ​​Мона Лиза Леонардо да Винчи?",
          answers: [
            {
              text: "Лувр, Париж, Франция",
              is_correct: true,
            },
            {
              text: "Третьяковская галлерея Москва Россия",
              is_correct: false,
            },
            {
              text: "Эрмитаж СПБ Россия",
              is_correct: false,
            },
            {
              text: "Старый музей Берлин Германия",
              is_correct: false,
            },
          ],
        },
      ],
      results: [
        {
          min: 0,
          max: 2,
          title: "Попробуйте снова!",
          desc: "Вы ответили не правильно на большинство вопросов, попробуйте почитать книги!",
        },
        {
          min: 25,
          max: 26,
          title: "Молодец ты ответил на большинство вопросов!",
          desc: "Изучай новое и для тебя не будет ничего невозможного!",
        },
      ],
    };
  },
  components: {
    Question,
    Result,
  },
  methods: {
    questionAnswered(is_correct) {
      if (is_correct) {
        this.totalCorrect++;
        console.log('Right')
      }
      else{
        console.log('not')
      }
      this.questionsAnswered++;
    },
    reset() {
      this.questionsAnswered = 0;
      this.totalCorrect = 0;
    },
  },
};
</script>





