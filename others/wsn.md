<div style="font-size: 22px; padding: 0 15px 0;">
  <div style="padding-bottom: 24px">WSN 无线传感器网络 笔记</div>
  <div style="background: #e5e6e8; height: 1px; margin-bottom: 20px;"></div>
</div>

![wsn.png](https://i.loli.net/2020/01/02/rxnMS4tpou83Fl2.png)

<ul style="list-style: disc outside;">
  <li style="line-height: 34px;"><span class="content mubu-node" heading="1"
      style="line-height: 34px; min-height: 34px; font-size: 24px; padding: 2px 0px; display: inline-block; vertical-align: top;">1&nbsp;介绍</span>
    <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
      <li style="line-height: 24px;"><span class="content mubu-node"
          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">略</span>
      </li>
    </ul>
  </li>
  <li style="line-height: 34px;"><span class="content mubu-node" heading="1"
      style="line-height: 34px; min-height: 34px; font-size: 24px; padding: 2px 0px; display: inline-block; vertical-align: top;">2&nbsp;物理层</span>
    <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
      <li style="line-height: 24px;"><span class="content mubu-node"
          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">面临的挑战</span>
        <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">有限的带宽</span>
          </li>
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">有限的传输范围</span>
          </li>
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">信号衰减</span>
          </li>
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">多径散射</span>
          </li>
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">干扰</span>
          </li>
        </ul>
      </li>
      <li style="line-height: 30px;"><span class="content mubu-node" heading="2"
          style="line-height: 30px; min-height: 30px; font-size: 21px; padding: 2px 0px; display: inline-block; vertical-align: top;">信源编码</span>
        <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">将模拟信号转化为数字信号</span>
          </li>
        </ul>
      </li>
      <li style="line-height: 30px;"><span class="content mubu-node" heading="2"
          style="line-height: 30px; min-height: 30px; font-size: 21px; padding: 2px 0px; display: inline-block; vertical-align: top;">信道编码</span>
        <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">减轻（或消除）噪声和干扰对数字信号传输的影响，增强鲁棒性</span>
            <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">检测与校正</span>
              </li>
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">前向纠错与重传</span>
              </li>
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">冗余编码</span>
              </li>
            </ul>
          </li>
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">提供错误检测以及前向纠错&nbsp;(FEC)&nbsp;机制</span>
          </li>
        </ul>
      </li>
      <li style="line-height: 30px;"><span class="content mubu-node" heading="2"
          style="line-height: 30px; min-height: 30px; font-size: 21px; padding: 2px 0px; display: inline-block; vertical-align: top;">调制</span>
        <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">将基带信号转换为带通信号</span>
          </li>
        </ul>
      </li>
      <li style="line-height: 30px;"><span class="content mubu-node" heading="2"
          style="line-height: 30px; min-height: 30px; font-size: 21px; padding: 2px 0px; display: inline-block; vertical-align: top;">香农公式</span>
        <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">C&nbsp;=&nbsp;B·log2(S/N)</span>
          </li>
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">信噪比&nbsp;SNR&nbsp;=&nbsp;S/N</span>
          </li>
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">SNRdb&nbsp;=&nbsp;10
              · log10(SNR)</span></li>
          <li style="line-height: 24px;"><span class="content mubu-node"
              images="%5B%7B%22id%22%3A%2214216f080b18730a8-2105618%22%2C%22oh%22%3A70%2C%22ow%22%3A301%2C%22uri%22%3A%22document_image%2F14607e03-5ecd-4cd2-8d65-bc2aa8f8c229-2105618.jpg%22%2C%22w%22%3A212%7D%5D"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">信干噪比</span>
            <div style="padding: 3px 0"><img
                src="https://img.mubu.com/document_image/14607e03-5ecd-4cd2-8d65-bc2aa8f8c229-2105618.jpg"
                style="max-width: 720px; width: 212px;" class="attach-img"></div>
          </li>
        </ul>
      </li>
      <li style="line-height: 24px;"><span class="content mubu-node"
          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">路径损耗</span>
      </li>
      <li style="line-height: 24px;"><span class="content mubu-node"
          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">遮蔽</span>
      </li>
      <li style="line-height: 24px;"><span class="content mubu-node"
          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">多径衰落</span>
      </li>
    </ul>
  </li>
  <li style="line-height: 34px;"><span class="content mubu-node" heading="1"
      style="line-height: 34px; min-height: 34px; font-size: 24px; padding: 2px 0px; display: inline-block; vertical-align: top;">3&nbsp;MAC协议</span>
    <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
      <li style="line-height: 24px;"><span class="content mubu-node"
          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">多用户环境下介质访问控制技术</span>
      </li>
      <li style="line-height: 30px;"><span class="content mubu-node" heading="2"
          style="line-height: 30px; min-height: 30px; font-size: 21px; padding: 2px 0px; display: inline-block; vertical-align: top;">信道访问控制方式</span>
        <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
          <li style="line-height: 27px;"><span class="content mubu-node" heading="3"
              style="line-height: 27px; min-height: 27px; font-size: 19px; padding: 2px 0px; display: inline-block; vertical-align: top;">基于分配</span>
            <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">固定信道分配</span>
                <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">FDMA&nbsp;频分多址接入</span><br><span
                      class="note"
                      style="display: inline-block; color: rgb(136, 136, 136); line-height: 22px; min-height: 22px; font-size: 14px; padding-bottom: 2px;">Frequency&nbsp;</span>
                  </li>
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">TDMA&nbsp;时分多址接入</span><br><span
                      class="note"
                      style="display: inline-block; color: rgb(136, 136, 136); line-height: 22px; min-height: 22px; font-size: 14px; padding-bottom: 2px;">Time&nbsp;</span>
                  </li>
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">CDMA&nbsp;码分多址接入</span><br><span
                      class="note"
                      style="display: inline-block; color: rgb(136, 136, 136); line-height: 22px; min-height: 22px; font-size: 14px; padding-bottom: 2px;">Code&nbsp;</span>
                  </li>
                </ul>
              </li>
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">动态信道分配</span>
                <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">轮询</span>
                  </li>
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">令牌环</span>
                  </li>
                </ul>
              </li>
            </ul>
          </li>
          <li style="line-height: 27px;"><span class="content mubu-node" heading="3"
              style="line-height: 27px; min-height: 27px; font-size: 19px; padding: 2px 0px; display: inline-block; vertical-align: top;">基于竞争</span>
            <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">ALOHA</span>
                <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">随机等待时间</span>
                  </li>
                </ul>
              </li>
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">CSMA
                  载波监听多路访问</span><br><span class="note"
                  style="display: inline-block; color: rgb(136, 136, 136); line-height: 22px; min-height: 22px; font-size: 14px; padding-bottom: 2px;">Carrier&nbsp;Sense&nbsp;Multiple&nbsp;Access</span>
                <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">CSMA/CA
                      碰撞避免</span><br><span class="note"
                      style="display: inline-block; color: rgb(136, 136, 136); line-height: 22px; min-height: 22px; font-size: 14px; padding-bottom: 2px;">CA
                      - Collsion Avoidance</span>
                    <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                      <li style="line-height: 24px;"><span class="content mubu-node"
                          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">IEEE&nbsp;802.11&nbsp;MAC&nbsp;很常用</span>
                      </li>
                      <li style="line-height: 24px;"><span class="content mubu-node"
                          images="%5B%7B%22id%22%3A%225516f075753c906a-2105618%22%2C%22oh%22%3A312%2C%22ow%22%3A460%2C%22uri%22%3A%22document_image%2F3bc81005-44e7-48c4-9805-74034e04f6c7-2105618.jpg%22%2C%22w%22%3A242%7D%2C%7B%22id%22%3A%225516f075753c906a-2105618%22%2C%22oh%22%3A312%2C%22ow%22%3A460%2C%22uri%22%3A%22document_image%2F3bc81005-44e7-48c4-9805-74034e04f6c7-2105618.jpg%22%7D%5D"
                          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">选择Wmax</span>
                        <div style="padding: 3px 0"><img
                            src="https://img.mubu.com/document_image/3bc81005-44e7-48c4-9805-74034e04f6c7-2105618.jpg"
                            style="max-width: 720px; width: 242px;" class="attach-img"></div>
                      </li>
                    </ul>
                  </li>
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">CSMA/CD
                      冲突检测</span><br><span class="note"
                      style="display: inline-block; color: rgb(136, 136, 136); line-height: 22px; min-height: 22px; font-size: 14px; padding-bottom: 2px;">Collision
                      Detection</span></li>
                </ul>
              </li>
            </ul>
          </li>
        </ul>
      </li>
      <li style="line-height: 24px;"><span class="content mubu-node"
          images="%5B%7B%22id%22%3A%2229916f075bcecf0ad-2105618%22%2C%22oh%22%3A169%2C%22ow%22%3A274%2C%22uri%22%3A%22document_image%2F23762021-1d97-4ab3-b2bf-9543844aba6d-2105618.jpg%22%7D%5D"
          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">隐藏终端（可以解决）</span>
        <div style="padding: 3px 0"><img
            src="https://img.mubu.com/document_image/23762021-1d97-4ab3-b2bf-9543844aba6d-2105618.jpg"
            style="max-width: 720px;" class="attach-img"></div>
        <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">由于监听到的信道空闲而不是真的空闲，故引发冲突</span>
          </li>
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">解决方法：进行一次握手（RTS、CTS）</span>
          </li>
        </ul>
      </li>
      <li style="line-height: 24px;"><span class="content mubu-node"
          images="%5B%7B%22id%22%3A%223e616f075bee0b0a9-2105618%22%2C%22oh%22%3A149%2C%22ow%22%3A262%2C%22uri%22%3A%22document_image%2F79e9be3c-6d13-44f2-80f1-0a0ac7227e92-2105618.jpg%22%7D%5D"
          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">暴露终端（解决不了）</span>
        <div style="padding: 3px 0"><img
            src="https://img.mubu.com/document_image/79e9be3c-6d13-44f2-80f1-0a0ac7227e92-2105618.jpg"
            style="max-width: 720px;" class="attach-img"></div>
        <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">由于监听到的信道忙而不是真的忙，故其可以传输而不传输</span>
          </li>
        </ul>
      </li>
      <li style="line-height: 30px;"><span class="content mubu-node" heading="2"
          style="line-height: 30px; min-height: 30px; font-size: 21px; padding: 2px 0px; display: inline-block; vertical-align: top;">WSN&nbsp;MAC</span>
        <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
          <li style="line-height: 27px;"><span class="content mubu-node" heading="3"
              style="line-height: 27px; min-height: 27px; font-size: 19px; padding: 2px 0px; display: inline-block; vertical-align: top;">基于竞争</span>
            <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">S-MAC</span><br><span
                  class="note"
                  style="display: inline-block; color: rgb(136, 136, 136); line-height: 22px; min-height: 22px; font-size: 14px; padding-bottom: 2px;">周期性侦听/睡眠调度</span>
                <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">周期性侦听/睡眠的工作方式（能量）</span>
                  </li>
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">一致性的睡眠调度机制（空闲侦听）</span>
                  </li>
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">流量自适应的侦听机制（减少延迟）</span>
                  </li>
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">消息分割和突发传递（控制消息和消息延迟）</span>
                  </li>
                </ul>
              </li>
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">T-MAC</span><br><span
                  class="note"
                  style="display: inline-block; color: rgb(136, 136, 136); line-height: 22px; min-height: 22px; font-size: 14px; padding-bottom: 2px;">流量自适应的侦听/睡眠调度</span>
                <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      images="%5B%7B%22id%22%3A%2218216f0761e235069-2105618%22%2C%22oh%22%3A258%2C%22ow%22%3A570%2C%22uri%22%3A%22document_image%2F024d1b09-c40e-4beb-b79a-35c9d8480615-2105618.jpg%22%2C%22w%22%3A247%7D%5D"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">S-MAC改进</span>
                    <div style="padding: 3px 0"><img
                        src="https://img.mubu.com/document_image/024d1b09-c40e-4beb-b79a-35c9d8480615-2105618.jpg"
                        style="max-width: 720px; width: 247px;" class="attach-img">
                    </div>
                  </li>
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      images="%5B%7B%22id%22%3A%2223016f076490a415e-2105618%22%2C%22oh%22%3A227%2C%22ow%22%3A550%2C%22uri%22%3A%22document_image%2F725d5f4e-2857-4d76-9e1b-764209ea6bd8-2105618.jpg%22%2C%22w%22%3A247%7D%5D"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">RTS→CTS→DATA→ACK</span>
                    <div style="padding: 3px 0"><img
                        src="https://img.mubu.com/document_image/725d5f4e-2857-4d76-9e1b-764209ea6bd8-2105618.jpg"
                        style="max-width: 720px; width: 247px;" class="attach-img">
                    </div>
                  </li>
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">根据通信流量动态调整活动的时间，用突发的方式发送信息，减少空闲侦听的时间</span>
                  </li>
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      images="%5B%7B%22id%22%3A%222716f07668d6b00b-2105618%22%2C%22oh%22%3A269%2C%22ow%22%3A671%2C%22uri%22%3A%22document_image%2F41c69c4c-1005-48a7-a3fe-1cad787bacbd-2105618.jpg%22%2C%22w%22%3A247%7D%5D"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">早睡问题</span>
                    <div style="padding: 3px 0"><img
                        src="https://img.mubu.com/document_image/41c69c4c-1005-48a7-a3fe-1cad787bacbd-2105618.jpg"
                        style="max-width: 720px; width: 247px;" class="attach-img">
                    </div>
                    <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                      <li style="line-height: 24px;"><span class="content mubu-node"
                          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">未来发送请求</span>
                      </li>
                      <li style="line-height: 24px;"><span class="content mubu-node"
                          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">满缓冲区优先</span>
                      </li>
                    </ul>
                  </li>
                </ul>
              </li>
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">Sift-MAC</span>
                <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">原理</span>
                    <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                      <li style="line-height: 24px;"><span class="content mubu-node"
                          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">采用CW值固定的窗口</span>
                      </li>
                      <li style="line-height: 24px;"><span class="content mubu-node"
                          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">不等概率选择时槽，在不同时槽采用不同选择概率</span>
                      </li>
                    </ul>
                  </li>
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">适用于分簇结构</span>
                  </li>
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">以簇头一直处于侦听状态换取较低延迟</span>
                  </li>
                </ul>
              </li>
            </ul>
          </li>
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">基于时分复用（TDMA）</span>
            <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">缺点</span>
                <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">要求严格的时间同步</span>
                  </li>
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">网络扩展性不好</span>
                  </li>
                </ul>
              </li>
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">基于分簇</span>
              </li>
            </ul>
          </li>
        </ul>
      </li>
    </ul>
  </li>
  <li style="line-height: 34px;"><span class="content mubu-node" heading="1"
      style="line-height: 34px; min-height: 34px; font-size: 24px; padding: 2px 0px; display: inline-block; vertical-align: top;">4&nbsp;WSN路由协议</span><br><span
      class="note"
      style="display: inline-block; color: rgb(136, 136, 136); line-height: 22px; min-height: 22px; font-size: 14px; padding-bottom: 2px;">​是一套将数据从源节点传输到目的机制​​</span>
    <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
      <li style="line-height: 24px;"><span class="content mubu-node"
          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">特点</span>
        <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">自组织的网络（随机部署）</span>
          </li>
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">数据的冗余性（多节点监测同一事件）</span>
          </li>
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">基于局部拓扑信息（硬件限制）</span>
          </li>
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">网络功能（数据收集）</span>
          </li>
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">以数据为中心</span>
          </li>
        </ul>
      </li>
      <li style="line-height: 30px;"><span class="content mubu-node" heading="2"
          style="line-height: 30px; min-height: 30px; font-size: 21px; padding: 2px 0px; display: inline-block; vertical-align: top;">平面路由协议</span>
        <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
          <li style="line-height: 27px;"><span class="content mubu-node" heading="3"
              style="line-height: 27px; min-height: 27px; font-size: 19px; padding: 2px 0px; display: inline-block; vertical-align: top;">DD路由算法
              Directed Diffusion</span><br><span class="note"
              style="display: inline-block; color: rgb(136, 136, 136); line-height: 22px; min-height: 22px; font-size: 14px; padding-bottom: 2px;">基于查询的路由</span>
            <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">兴趣扩散</span>
                <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">Sink汇聚节点发送兴趣消息洪泛给其他节点</span>
                  </li>
                </ul>
              </li>
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">梯度建立</span>
                <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">成本最小化</span>
                  </li>
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">信息梯度</span>
                    <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                      <li style="line-height: 24px;"><span class="content mubu-node"
                          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">包含下一跳节点、时间戳、信息采集相关内容</span>
                      </li>
                    </ul>
                  </li>
                </ul>
              </li>
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">数据传播</span>
              </li>
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">路径加强</span>
              </li>
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">优点</span>
                <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">数据中心路由，定义不同任务类型/目标区域消息</span>
                  </li>
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">路径加强机制可显著提高数据传输的速率</span>
                  </li>
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">周期性路由：能量的均衡消耗</span>
                  </li>
                </ul>
              </li>
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">缺点</span>
                <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">周期性的洪泛机制:
                      能量和时间开销都比较大</span></li>
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">节点需要维护一个兴趣消息列表，代价较大</span>
                  </li>
                </ul>
              </li>
            </ul>
          </li>
          <li style="line-height: 27px;"><span class="content mubu-node" heading="3"
              style="line-height: 27px; min-height: 27px; font-size: 19px; padding: 2px 0px; display: inline-block; vertical-align: top;">能量感知路由</span><br><span
              class="note"
              style="display: inline-block; color: rgb(136, 136, 136); line-height: 22px; min-height: 22px; font-size: 14px; padding-bottom: 2px;">基于节点的可用能量（PowerAvailable，PA）或传输路径上链路的能量需求选择数据的发送路径</span>
            <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">可用能量（Power
                  Available，PA）</span></li>
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">目标</span>
                <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">均衡消耗节点能量增加网络的生存期，根据节点的可用能量或传输路径上的能量需求，选择数据转发路径</span>
                  </li>
                </ul>
              </li>
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">方法</span>
                <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">在源和目的之间建立多条路径，根据能量因素给每条路径赋予被选择使用的概率</span>
                  </li>
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">在发送数据时，基于概率随机选择其中的一条路径</span>
                  </li>
                </ul>
              </li>
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">结果</span>
                <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">没有一条路径一直在传送数据，防止一条路径上节点能量消耗过快</span>
                  </li>
                </ul>
              </li>
            </ul>
          </li>
        </ul>
      </li>
      <li style="line-height: 30px;"><span class="content mubu-node" heading="2"
          style="line-height: 30px; min-height: 30px; font-size: 21px; padding: 2px 0px; display: inline-block; vertical-align: top;">集群结构的路由协议</span><br><span
          class="note"
          style="display: inline-block; color: rgb(136, 136, 136); line-height: 22px; min-height: 22px; font-size: 14px; padding-bottom: 2px;">网络分层路由</span>
        <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
          <li style="line-height: 27px;"><span class="content mubu-node" heading="3"
              style="line-height: 27px; min-height: 27px; font-size: 19px; padding: 2px 0px; display: inline-block; vertical-align: top;">LEACH</span>
            <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
              <li style="line-height: 24px;"><span class="content mubu-node"
                  images="%5B%7B%22id%22%3A%2214416f078bf65209b-2105618%22%2C%22oh%22%3A85%2C%22ow%22%3A332%2C%22uri%22%3A%22document_image%2F7d59d5ea-caa8-4c2e-860e-9b1073300155-2105618.jpg%22%7D%5D"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">簇头选择算法</span>
                <div style="padding: 3px 0"><img
                    src="https://img.mubu.com/document_image/7d59d5ea-caa8-4c2e-860e-9b1073300155-2105618.jpg"
                    style="max-width: 720px;" class="attach-img"></div>
                <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">节点随机产生一个0~1的数</span>
                  </li>
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      images="%5B%7B%22id%22%3A%22c716f07a551580bb-2105618%22%2C%22oh%22%3A95%2C%22ow%22%3A313%2C%22uri%22%3A%22document_image%2F1718bfa1-b949-40d6-8085-eaf7d0bd0fdc-2105618.jpg%22%2C%22w%22%3A202%7D%5D"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">数值小于T(n)则称为head簇头（未当选过）</span>
                    <div style="padding: 3px 0"><img
                        src="https://img.mubu.com/document_image/1718bfa1-b949-40d6-8085-eaf7d0bd0fdc-2105618.jpg"
                        style="max-width: 720px; width: 202px;" class="attach-img">
                    </div>
                    <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                      <li style="line-height: 24px;"><span class="content mubu-node"
                          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">P:
                          需要的Head的百分比</span></li>
                      <li style="line-height: 24px;"><span class="content mubu-node"
                          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">r:
                          当前round</span></li>
                      <li style="line-height: 24px;"><span class="content mubu-node"
                          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">n:
                          节点（n∈G）</span></li>
                      <li style="line-height: 24px;"><span class="content mubu-node"
                          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">G:
                          没有做过Head的节点集合</span></li>
                    </ul>
                  </li>
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">每个Head使用CSMA
                      MAC协议通知全体节点，包含自己的ID</span></li>
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">节点就近选择Head，通过CSMA发送加入请求，包含自己的ID</span>
                  </li>
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">使用TDMA（时分复用）调度信息</span>
                  </li>
                </ul>
              </li>
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">优点</span>
                <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">优化了传输数据所需能量</span>
                  </li>
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">优化了网络中的数据量</span>
                  </li>
                </ul>
              </li>
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">缺点</span>
                <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">节点硬件需要支持射频功率自适应调整</span>
                  </li>
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">无法保证簇头节点能遍及整个网络</span>
                  </li>
                </ul>
              </li>
            </ul>
          </li>
        </ul>
      </li>
      <li style="line-height: 30px;"><span class="content mubu-node" heading="2"
          style="line-height: 30px; min-height: 30px; font-size: 21px; padding: 2px 0px; display: inline-block; vertical-align: top;">地理信息路由协议</span>
        <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
          <li style="line-height: 27px;"><span class="content mubu-node" heading="3"
              style="line-height: 27px; min-height: 27px; font-size: 19px; padding: 2px 0px; display: inline-block; vertical-align: top;">GEAR路由</span>
            <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">应用</span>
                <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">到特定区域的路由</span>
                  </li>
                </ul>
              </li>
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">前提</span>
                <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">已知目标区域的位置信息</span>
                  </li>
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">节点知道自己位置信息和剩余能量</span>
                  </li>
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">节点间无线链路是对称的</span>
                  </li>
                </ul>
              </li>
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">两步路由</span><br><span
                  class="note"
                  style="display: inline-block; color: rgb(136, 136, 136); line-height: 22px; min-height: 22px; font-size: 14px; padding-bottom: 2px;">将查询命令传输到查询区域​查询区域内传输到所有节点</span>
              </li>
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">选路依据
                  F (N, R) = a · Distance(N, R) + (1 - a) · Left_Energy(N)</span></li>
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">传送方式</span>
                <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">洪泛（节点较少）</span>
                  </li>
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">迭代地理转发（节点较多时效果好点）</span>
                  </li>
                </ul>
              </li>
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">路由空洞</span>
              </li>
            </ul>
          </li>
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">GSPR</span>
          </li>
        </ul>
      </li>
      <li style="line-height: 24px;"><span class="content mubu-node"
          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">其他</span>
        <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">多路径</span>
          </li>
        </ul>
      </li>
    </ul>
  </li>
  <li style="line-height: 34px;"><span class="content mubu-node" heading="1"
      style="line-height: 34px; min-height: 34px; font-size: 24px; padding: 2px 0px; display: inline-block; vertical-align: top;">5&nbsp;WSN拓扑控制</span>
    <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
      <li style="line-height: 27px;"><span class="content mubu-node" heading="3"
          style="line-height: 27px; min-height: 27px; font-size: 19px; padding: 2px 0px; display: inline-block; vertical-align: top;">节点功率控制</span><br><span
          class="note"
          style="display: inline-block; color: rgb(136, 136, 136); line-height: 22px; min-height: 22px; font-size: 14px; padding-bottom: 2px;">动态调整节点的发送功率，在保证网络拓扑结构连通需求的基础上，降低节点的发送功率，延长整个网络的生存时间。当传感器节点部署在二维或三维空间中，功率控制问题是一个NP难的问题</span>
        <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">基于节点度的算法</span><br><span
              class="note"
              style="display: inline-block; color: rgb(136, 136, 136); line-height: 22px; min-height: 22px; font-size: 14px; padding-bottom: 2px;">节点度:节点单跳邻居节点的个数</span>
            <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">本地平均算法
                  LMA</span>
                <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">检查邻居个数，控制在一个范围内</span>
                  </li>
                </ul>
              </li>
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">本地邻居平均算法
                  LMN</span>
                <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">相比LMA，将邻居个数放入自己的信息中，然后将所有邻居的邻居数求平均值作为自己的邻居数</span>
                  </li>
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">即“自己的邻居平均有多少邻居”</span>
                  </li>
                </ul>
              </li>
            </ul>
          </li>
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">基于邻近图的算法</span>
          </li>
        </ul>
      </li>
      <li style="line-height: 24px;"><span class="content mubu-node"
          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">睡眠调度</span>
      </li>
      <li style="line-height: 24px;"><span class="content mubu-node"
          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">层次型拓扑结构</span>
        <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">LEACH</span>
          </li>
        </ul>
      </li>
      <li style="line-height: 24px;"><span class="content mubu-node"
          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">作用</span>
        <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">可以延长WSN的生命周期</span>
          </li>
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">可有效减弱节点间通信干扰，
              提高通信效率</span></li>
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">为路由协议的实施提供基础数据</span>
          </li>
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">可以更好地进行数据融合及有利于提高网络的鲁棒性&nbsp;</span>
          </li>
        </ul>
      </li>
    </ul>
  </li>
  <li style="line-height: 34px;"><span class="content mubu-node" heading="1"
      style="line-height: 34px; min-height: 34px; font-size: 24px; padding: 2px 0px; display: inline-block; vertical-align: top;">6&nbsp;定位技术</span>
    <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
      <li style="line-height: 24px;"><span class="content mubu-node"
          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">计算节点位置</span>
        <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">三边测量估计法</span>
            <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
              <li style="line-height: 24px;"><span class="content mubu-node"
                  images="%5B%7B%22id%22%3A%2217e16f07ad6fb5118-2105618%22%2C%22oh%22%3A126%2C%22ow%22%3A382%2C%22uri%22%3A%22document_image%2F7f6bdca8-85f4-4eb5-a76b-d4089aae7670-2105618.jpg%22%2C%22w%22%3A369%7D%5D"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">已知A、B、C三个节点的坐标，以及它们到节点D的距离</span>
                <div style="padding: 3px 0"><img
                    src="https://img.mubu.com/document_image/7f6bdca8-85f4-4eb5-a76b-d4089aae7670-2105618.jpg"
                    style="max-width: 720px; width: 369px;" class="attach-img"></div>
              </li>
            </ul>
          </li>
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">三角测量估计法</span>
            <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
              <li style="line-height: 24px;"><span class="content mubu-node"
                  images="%5B%7B%22id%22%3A%2229316f07b08f0c0eb%22%2C%22oh%22%3A225%2C%22ow%22%3A694%2C%22uri%22%3A%22document_image%2F9ca5987e-2e23-4a50-b0e5-f65d49d4d82a-2105618.jpg%22%2C%22w%22%3A489%7D%5D"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">已知A、B、C三个节点的坐标、节点D相对于节点A、B、C的角度</span>
                <div style="padding: 3px 0"><img
                    src="https://img.mubu.com/document_image/9ca5987e-2e23-4a50-b0e5-f65d49d4d82a-2105618.jpg"
                    style="max-width: 720px; width: 489px;" class="attach-img"></div>
              </li>
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">转化为三边测量（图中三条虚线长度相等作为圆半径，应用余弦定理）</span>
              </li>
            </ul>
          </li>
          <li style="line-height: 24px;"><span class="content mubu-node"
              images="%5B%7B%22id%22%3A%223e716f07bd8735177-2105618%22%2C%22oh%22%3A103%2C%22ow%22%3A392%2C%22uri%22%3A%22document_image%2Fe63e737c-b7b4-48ac-a62e-a493e09d695a-2105618.jpg%22%7D%5D"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">极大似然估计法</span>
            <div style="padding: 3px 0"><img
                src="https://img.mubu.com/document_image/e63e737c-b7b4-48ac-a62e-a493e09d695a-2105618.jpg"
                style="max-width: 720px;" class="attach-img"></div>
          </li>
        </ul>
      </li>
      <li style="line-height: 24px;"><span class="content mubu-node"
          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">WSN定位机制</span>
        <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">基于距离的定位机制</span>
            <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">TOA</span><br><span
                  class="note"
                  style="display: inline-block; color: rgb(136, 136, 136); line-height: 22px; min-height: 22px; font-size: 14px; padding-bottom: 2px;">已知信号的传播速度，根据信号的传播时间来计算节点间的距离，然后利用三边或者极大似然估计法等计算出节点的位置</span>
              </li>
              <li style="line-height: 24px;"><span class="content mubu-node"
                  images="%5B%7B%22id%22%3A%2233816f07c1153a151-2105618%22%2C%22oh%22%3A165%2C%22ow%22%3A492%2C%22uri%22%3A%22document_image%2Ff2e798f9-03f7-49de-8b0e-750c2b2a9dd9-2105618.jpg%22%7D%5D"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">TDOA</span>
                <div style="padding: 3px 0"><img
                    src="https://img.mubu.com/document_image/f2e798f9-03f7-49de-8b0e-750c2b2a9dd9-2105618.jpg"
                    style="max-width: 720px;" class="attach-img"></div><br><span class="note"
                  style="display: inline-block; color: rgb(136, 136, 136); line-height: 22px; min-height: 22px; font-size: 14px; padding-bottom: 2px;">发送节点同时发送两种不同传播速度的无线信号，接收节点根据两种信号到达时间差以及已知这两种信号的传播速度，计算两个节点之间的距离，再通过已有基本的定位算法计算出节点的位置​</span>
                <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">推导方式</span>
                    <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                      <li style="line-height: 24px;"><span class="content mubu-node"
                          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">C1
                          = Dist / T1</span></li>
                      <li style="line-height: 24px;"><span class="content mubu-node"
                          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">C2
                          = Dist / T2</span></li>
                      <li style="line-height: 24px;"><span class="content mubu-node"
                          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">1/C2
                          - 1/C1 = (1/Dist)·(T2 - T1)</span></li>
                      <li style="line-height: 24px;"><span class="content mubu-node"
                          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">Dist
                          = (T2 - T1) · ( C1·C2 / (C1 - C2) )</span></li>
                    </ul>
                  </li>
                </ul>
              </li>
            </ul>
          </li>
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">距离无关的定位机制</span>
            <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">DV-Hop
                  距离向量-跳段定位算法</span>
                <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">基本思想</span>
                    <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                      <li style="line-height: 24px;"><span class="content mubu-node"
                          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">计算未知节点与信标节点的最小跳数</span>
                        <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                          <li style="line-height: 24px;"><span class="content mubu-node"
                              images="%5B%7B%22id%22%3A%2224d16f07ce3107085-2105618%22%2C%22oh%22%3A179%2C%22ow%22%3A173%2C%22uri%22%3A%22document_image%2Fad72ddb6-083d-49c4-b175-798a0f69a671-2105618.jpg%22%7D%5D"
                              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">跳数类似于同心圆传播（数字为跳数）</span>
                            <div style="padding: 3px 0"><img
                                src="https://img.mubu.com/document_image/ad72ddb6-083d-49c4-b175-798a0f69a671-2105618.jpg"
                                style="max-width: 720px;" class="attach-img">
                            </div>
                          </li>
                        </ul>
                      </li>
                      <li style="line-height: 24px;"><span class="content mubu-node"
                          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">估计平均每跳的距离</span>
                        <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                          <li style="line-height: 24px;"><span class="content mubu-node"
                              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">每个信标节点根据记录的其他信标节点的位置信息和相距跳数，估计平均每跳的实际距离</span>
                          </li>
                          <li style="line-height: 24px;"><span class="content mubu-node"
                              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">信标节点将计算的每跳平均距离用带有生存周期字段的分组广播至网络中，未知节点仅<span
                                class="bold" style="font-weight: bold;">仅</span>记录接收到的第一个每跳平均距离，并转发给邻居节点</span>
                          </li>
                        </ul>
                      </li>
                      <li style="line-height: 24px;"><span class="content mubu-node"
                          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">利用最小跳数乘以平均每跳距离，得到未知节点与信标节点之间的估计距离</span>
                      </li>
                      <li style="line-height: 24px;"><span class="content mubu-node"
                          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">利用三边测量法或极大似然估计法计算未知节点的坐标</span>
                      </li>
                    </ul>
                  </li>
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      images="%5B%7B%22id%22%3A%22d016f07d4df01025-2105618%22%2C%22oh%22%3A238%2C%22ow%22%3A362%2C%22uri%22%3A%22document_image%2Fd12f8fb2-bad7-41ba-a502-5e4133ce237a-2105618.jpg%22%2C%22w%22%3A234%7D%5D"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">例子</span>
                    <div style="padding: 3px 0"><img
                        src="https://img.mubu.com/document_image/d12f8fb2-bad7-41ba-a502-5e4133ce237a-2105618.jpg"
                        style="max-width: 720px; width: 234px;" class="attach-img">
                    </div>
                    <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                      <li style="line-height: 24px;"><span class="content mubu-node"
                          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">信标节点L2计算的每跳平均距离为
                          (40+75) / (2+5)</span></li>
                      <li style="line-height: 24px;"><span class="content mubu-node"
                          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">A从L2获得每跳平均距离（L2离A最近），则节点A与三个信标节点之间的距离分别为</span>
                        <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                          <li style="line-height: 24px;"><span class="content mubu-node"
                              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">L1：3*16.42</span>
                          </li>
                          <li style="line-height: 24px;"><span class="content mubu-node"
                              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">L2：2*16.42</span>
                          </li>
                          <li style="line-height: 24px;"><span class="content mubu-node"
                              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">L3：3*16.42</span>
                          </li>
                        </ul>
                      </li>
                    </ul>
                  </li>
                </ul>
              </li>
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">APIT
                  近似三角形内点测试算法</span><br><span class="note"
                  style="display: inline-block; color: rgb(136, 136, 136); line-height: 22px; min-height: 22px; font-size: 14px; padding-bottom: 2px;">Approximate
                  Point-In-Triangulation Test</span>
                <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">基本思想</span>
                    <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                      <li style="line-height: 24px;"><span class="content mubu-node"
                          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">首先确定多个包含未知节点的三角形区域</span>
                      </li>
                      <li style="line-height: 24px;"><span class="content mubu-node"
                          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">这些三角形区域的交集是一个多边形，它确定了更小的包含未知节点的区域</span>
                      </li>
                      <li style="line-height: 24px;"><span class="content mubu-node"
                          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">计算这个多边形区域的质心，并将质心作为未知节点的位置</span>
                      </li>
                    </ul>
                  </li>
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">原理
                      —— PIT原理</span>
                    <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                      <li style="line-height: 24px;"><span class="content mubu-node"
                          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">假如存在一个方向，节点M沿着这个方向移动会同时远离或接近顶点A、B、C，那么节点M位于三角形ABC外</span>
                      </li>
                      <li style="line-height: 24px;"><span class="content mubu-node"
                          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">否则，节点M位于三角形ABC内</span>
                      </li>
                    </ul>
                  </li>
                </ul>
              </li>
            </ul>
          </li>
        </ul>
      </li>
    </ul>
  </li>
  <li style="line-height: 34px;"><span class="content mubu-node" heading="1"
      style="line-height: 34px; min-height: 34px; font-size: 24px; padding: 2px 0px; display: inline-block; vertical-align: top;">7&nbsp;时间同步技术</span>
    <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
      <li style="line-height: 24px;"><span class="content mubu-node"
          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">按网络应用深度分类</span>
        <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">时序确定</span><br><span
              class="note"
              style="display: inline-block; color: rgb(136, 136, 136); line-height: 22px; min-height: 22px; font-size: 14px; padding-bottom: 2px;">判断事件发生的先后顺序，对本地时间的要求比较低，只需要知道本节点与其余节点的相对时间即可</span>
          </li>
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">相对同步</span><br><span
              class="note"
              style="display: inline-block; color: rgb(136, 136, 136); line-height: 22px; min-height: 22px; font-size: 14px; padding-bottom: 2px;">节点维护自己的本地时钟，周期性地获取其邻居节点与本节点的时钟偏移，实现本节点与邻居节点的时间同步</span>
          </li>
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">绝对同步</span><br><span
              class="note"
              style="display: inline-block; color: rgb(136, 136, 136); line-height: 22px; min-height: 22px; font-size: 14px; padding-bottom: 2px;">所有节点的本地时间严格同步，等同于标准时间，这种情况对节点的要求最高，因此实现也最为复杂</span>
          </li>
        </ul>
      </li>
      <li style="line-height: 24px;"><span class="content mubu-node"
          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">按参考时间来源分类</span>
        <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">外同步</span><br><span
              class="note"
              style="display: inline-block; color: rgb(136, 136, 136); line-height: 22px; min-height: 22px; font-size: 14px; padding-bottom: 2px;">标准参考时间来自于外部</span>
          </li>
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">内同步</span><br><span
              class="note"
              style="display: inline-block; color: rgb(136, 136, 136); line-height: 22px; min-height: 22px; font-size: 14px; padding-bottom: 2px;">参考时间来自于网络内部某个节点的时间</span>
          </li>
        </ul>
      </li>
      <li style="line-height: 24px;"><span class="content mubu-node"
          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">时间参数</span>
        <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">时钟偏移</span><br><span
              class="note"
              style="display: inline-block; color: rgb(136, 136, 136); line-height: 22px; min-height: 22px; font-size: 14px; padding-bottom: 2px;">本地时间与真实时间的差值</span>
          </li>
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">时钟漂移</span><br><span
              class="note"
              style="display: inline-block; color: rgb(136, 136, 136); line-height: 22px; min-height: 22px; font-size: 14px; padding-bottom: 2px;">本地时间变化速率与1的差值</span>
          </li>
        </ul>
      </li>
      <li style="line-height: 24px;"><span class="content mubu-node"
          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">时间计数方式</span>
        <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">硬件时钟模式</span><br><span
              class="note"
              style="display: inline-block; color: rgb(136, 136, 136); line-height: 22px; min-height: 22px; font-size: 14px; padding-bottom: 2px;">利用晶振来实现时间的计数</span>
          </li>
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">软件时钟模式</span><br><span
              class="note"
              style="display: inline-block; color: rgb(136, 136, 136); line-height: 22px; min-height: 22px; font-size: 14px; padding-bottom: 2px;">采用虚拟的软件时钟来实现时钟的计数</span>
          </li>
        </ul>
      </li>
      <li style="line-height: 24px;"><span class="content mubu-node"
          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">需要满足的要求</span>
        <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">能量有限</span>
          </li>
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">可扩展</span>
          </li>
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">稳定性</span>
          </li>
        </ul>
      </li>
      <li style="line-height: 24px;"><span class="content mubu-node"
          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">技术问题</span>
        <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
          <li style="line-height: 24px;"><span class="content mubu-node"
              images="%5B%7B%22id%22%3A%222bf16f07e4bf8901e-2105618%22%2C%22oh%22%3A169%2C%22ow%22%3A540%2C%22uri%22%3A%22document_image%2F38746e47-71c4-41be-9e47-e50da96d2e51-2105618.jpg%22%2C%22w%22%3A410%7D%5D"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">传播延迟不可预测</span>
            <div style="padding: 3px 0"><img
                src="https://img.mubu.com/document_image/38746e47-71c4-41be-9e47-e50da96d2e51-2105618.jpg"
                style="max-width: 720px; width: 410px;" class="attach-img"></div>
            <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">发送时间：发送方用于组装并将报文换交给发送方MAC层的时间</span>
              </li>
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">访问时间：指在发送方MAC层从获得报文后到获取无线信道发送权的等待时间</span>
              </li>
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">传送时间：发送方发送报文的时间，报文的第一个字节开始发送到发送完最后一个字节的时间</span>
              </li>
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">传播时间：报文从发送方以电磁波的形式传送到接收方所花费的时间</span>
              </li>
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">接收时间：接收方接收报文的时间。它和传送时间完全相同，具有确定性</span>
              </li>
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">接受时间：用于处理接收到的报文的时间</span>
              </li>
            </ul>
          </li>
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">高能效</span>
          </li>
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">可扩展、健壮</span>
          </li>
        </ul>
      </li>
      <li style="line-height: 24px;"><span class="content mubu-node"
          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">同步机制</span>
        <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">发送者-接收者同步模式</span><br><span
              class="note"
              style="display: inline-block; color: rgb(136, 136, 136); line-height: 22px; min-height: 22px; font-size: 14px; padding-bottom: 2px;">发送者发送带有时间戳的同步包给接收者，同步接收者的时间</span>
          </li>
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">接收者-接收者同步模式</span><br><span
              class="note"
              style="display: inline-block; color: rgb(136, 136, 136); line-height: 22px; min-height: 22px; font-size: 14px; padding-bottom: 2px;">多个接收者利用发送者发送的同步包在若干接收者之间进行同步，缩短了关键路径，避免发送者到接收者的关键路径过长而导致的不准确的传输延迟估计</span>
            <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">RBS
                  参考广播同步</span><br><span class="note"
                  style="display: inline-block; color: rgb(136, 136, 136); line-height: 22px; min-height: 22px; font-size: 14px; padding-bottom: 2px;">Reference
                  Broadcast Synchronization</span>
                <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">工作机制</span>
                    <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                      <li style="line-height: 24px;"><span class="content mubu-node"
                          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">发送节点周期性地向接收节点发送参考报文</span>
                      </li>
                      <li style="line-height: 24px;"><span class="content mubu-node"
                          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">广播域内的接收节点都将收到该参考报文，并各自记录收到该报文的时刻</span>
                      </li>
                      <li style="line-height: 24px;"><span class="content mubu-node"
                          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">接收者们通过交换本地时间戳信息，这样这一组节点就可以计算出它们之间的时钟偏差</span>
                      </li>
                    </ul>
                  </li>
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">RBS算法中广播的时间同步消息与真实的时间戳信息并无多大关系，它也不关心准确的发送和接收时间，而只关心报文传输的差值，RBS同步算法完全排除了发送时间和接收时间的干扰</span>
                  </li>
                </ul>
              </li>
            </ul>
          </li>
          <li style="line-height: 24px;"><span class="content mubu-node"
              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">TPSN
              双向报文交换协议</span><br><span class="note"
              style="display: inline-block; color: rgb(136, 136, 136); line-height: 22px; min-height: 22px; font-size: 14px; padding-bottom: 2px;">Timing-sync
              Protocol for Sensor Networks</span>
            <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
              <li style="line-height: 24px;"><span class="content mubu-node"
                  images="%5B%7B%22id%22%3A%222c116f07f3fb2508f-2105618%22%2C%22oh%22%3A303%2C%22ow%22%3A504%2C%22uri%22%3A%22document_image%2F48ab5f69-9351-42a8-9f81-75cedecdd5ad-2105618.jpg%22%2C%22w%22%3A277%7D%5D"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">层次发现阶段</span>
                <div style="padding: 3px 0"><img
                    src="https://img.mubu.com/document_image/48ab5f69-9351-42a8-9f81-75cedecdd5ad-2105618.jpg"
                    style="max-width: 720px; width: 277px;" class="attach-img"></div>
              </li>
              <li style="line-height: 24px;"><span class="content mubu-node"
                  style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">时间同步阶段</span>
                <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                  <li style="line-height: 24px;"><span class="content mubu-node"
                      images="%5B%7B%22id%22%3A%2225216f07f4ef03078-2105618%22%2C%22oh%22%3A205%2C%22ow%22%3A397%2C%22uri%22%3A%22document_image%2F3f203065-9054-4793-8511-c8ce5b38158b-2105618.jpg%22%2C%22w%22%3A252%7D%5D"
                      style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">双向报文机制</span>
                    <div style="padding: 3px 0"><img
                        src="https://img.mubu.com/document_image/3f203065-9054-4793-8511-c8ce5b38158b-2105618.jpg"
                        style="max-width: 720px; width: 252px;" class="attach-img">
                    </div>
                    <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                      <li style="line-height: 24px;"><span class="content mubu-node"
                          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">根据TPSN报文交换协议，我们规定T1和T4为节点A的时间，T2和T3为节点B的时间</span>
                      </li>
                      <li style="line-height: 24px;"><span class="content mubu-node"
                          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">节点A在T1向节点B发送一个同步报文</span>
                      </li>
                      <li style="line-height: 24px;"><span class="content mubu-node"
                          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">节点B在收到该报文后，记录下接收到该报文的时刻T2，并立刻向节点A发回一个应答报文，将时刻T2和该报文的发送时刻T3嵌入到应答报文中</span>
                      </li>
                      <li style="line-height: 24px;"><span class="content mubu-node"
                          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">当节点A收到该应答报文后，记录下此时刻T4</span>
                      </li>
                      <li style="line-height: 24px;"><span class="content mubu-node"
                          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">我们假设当节点A在T1时刻，A和B的时间偏移为Δ</span>
                      </li>
                      <li style="line-height: 24px;"><span class="content mubu-node"
                          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">因为T1到T4两个报文发送的时间非常短，我们可以认为Δ没有变化</span>
                      </li>
                      <li style="line-height: 24px;"><span class="content mubu-node"
                          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">假设报文的传输延迟都是相同且对称的，均为d，那么有</span>
                        <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                          <li style="line-height: 24px;"><span class="content mubu-node"
                              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">T2=T1+Δ+d</span>
                          </li>
                          <li style="line-height: 24px;"><span class="content mubu-node"
                              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">T4=T3−Δ+d</span>
                          </li>
                        </ul>
                      </li>
                      <li style="line-height: 24px;"><span class="content mubu-node"
                          style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">这两个方程联立可解得</span>
                        <ul class="children" style="list-style: disc outside; padding-bottom: 4px;">
                          <li style="line-height: 24px;"><span class="content mubu-node"
                              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">Δ
                              = [(T2 - T1) - (T4 - T3)] / 2</span></li>
                          <li style="line-height: 24px;"><span class="content mubu-node"
                              style="line-height: 24px; min-height: 24px; font-size: 16px; padding: 2px 0px; display: inline-block; vertical-align: top;">d
                              = [(T2 - T1) + (T4 - T3)] / 2</span></li>
                        </ul>
                      </li>
                    </ul>
                  </li>
                </ul>
              </li>
            </ul>
          </li>
        </ul>
      </li>
    </ul>
  </li>
</ul>