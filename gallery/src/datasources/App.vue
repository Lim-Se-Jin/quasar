<template>
  <v-app>
    <!-- 툴바에 제목과 버튼 삽입-->
    <v-app-bar app color = "blue-grey" dark fixed>
      <v-app-bar-nav-icon></v-app-bar-nav-icon>
      <v-toolbar-title>사진 갤러리</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn icon>
        <v-icon>more_vert</v-icon>
      </v-btn>
  </v-app-bar>
  <v-main>
    <v-container>
      <v-row>
        <!-- 기기별로 그리드의 크기 설정-->
        <v-col cols="12" sm="6" md="4" lg="3" xl="2"
          v-for="item in this.aPictures":key=item.key>
        <!--카드 UI에 사진 담아내기-->
        <v-card height="330px">
          <v-img :src="item.url" height="200px">
       </v-img>
        <v-card-title>
          <h1 class="title grey--text text--darken-3 mb-3">
            {{ item.title }} </h1>
            <p class="body-2 grey--text">{{ item.info }}</p>
            </v-card-title>
            </v-card>
        </v-col>
      </v-row>
    </v-container>
  </v-main>
  <!--바닥글 고정-->
  <v-footer fixed>
    <div class="mx-auto">&copy; CODE-DESIGN.web.app </div>
  </v-footer>
  </v-app>
</template>
