<script setup lang="ts">

</script>

<template>
  <footer>
    <div w-full flex justify-around gap-12 class="Footer-Community">
      <div class="Footer-Community-Column">
        <p>官方社区</p>

        <ul>
          <li>微信公众号</li>
          <li>小红书账号</li>
          <li>抖音账号</li>
          <li>飞书账号</li>
          <li>知乎账号</li>
          <li>GitHub账号</li>
          <li>微博账号</li>
        </ul>
      </div>
      <div class="Footer-Community-Column">
        <p>全部产品</p>

        <ul>
          <li>科塔智爱</li>
          <li>科塔惠编</li>
          <li>科塔锐意</li>
          <li>科塔拼拼</li>
          <li>科塔聚风</li>
          <li>科塔一览</li>
          <li>科塔一滴</li>
        </ul>
      </div>
      <div class="Footer-Community-Column">
        <p>相关服务</p>

        <ul>
          <li>技术支持</li>
          <li>售前咨询</li>
          <li>售后咨询</li>
          <li>相关协议</li>
          <li>代理商</li>
          <li>赞助商</li>
          <li>商务合作</li>
        </ul>
      </div>
    </div>

    <div w-full flex items-center justify-around class="Footer-Bottom">
      <div flex items-center class="logo">
        <img src="/favicon.svg">
        <h1 pr-38px text-4 font-bold>
          QuotaWish
        </h1>
      </div>
      <div flex flex-wrap class="info">
        <div class="copyright">
          Copyright © 2024 QuotaWish Inc.
        </div>
        <div>
          <a href="https://beian.miit.gov.cn/" target="_blank">蜀ICP备2024090189号</a>
        </div>
      </div>
    </div>
  </footer>
</template>

<style lang="scss" scoped>
.Footer-Bottom {
}

.Footer-Community-Column {
  display: flex;

  text-align: left;
  flex-direction: column;
  justify-content: flex-start;

  ul {
    li {
      &:hover {
        opacity: 1;
        color: #3ab8fd;
        cursor: pointer;
      }
      margin: 0.5rem 0;

      opacity: 0.75;
    }
  }

  p {
    margin: 1rem 0;
    font-weight: 600;
    font-size: 1.2em;
  }
}

@media (max-width: 768px) {
  div.info {
    flex-direction: column !important;
  }

  .copyright {
    display: none;
  }
}

info.div a {
  width: 200px;
}

div.logo {
  width: max-content;
  height: 128px;
}

div.logo img {
  width: 108px;
  height: 108px;
}

div.info {
  display: flex;
  justify-content: flex-start;
}

div.info > div {
  padding: 0 0.5rem;

  border-right: 2px solid #cfcdcd;
}

div.info > div:last-child {
  border-right: none;
}

footer {
  position: relative;
  padding: 0 10%;
  display: flex;

  flex-wrap: wrap;
  align-items: center;
  flex-direction: column;

  width: 100%;
  min-height: 200px;

  bottom: 0;

  font-size: 18px;
  text-align: center;
}
</style>
