---
layout: post
title: 接入网和骨干网
---

接入网和骨干网也是我们常见的两个网络概念。

接入网就像是我们日常生活中的接驳系统。无论你是通过手机、Wi-Fi、光纤，还是传统的电话拨号，都属于接入网的一部分。接入网为普通用户提供上网的入口，将数据从用户端传输到更大的骨干网。

而骨干网则是指网络的主干部分，像铁路中的主干线路一样，它为不同的接入网提供连接，确保数据流量能够高效地传输到全球其他地方。

骨干网是一个大型、高速的网络，它是各个子网之间连接的核心部分。可以将骨干网看作是整个通信网络的“高速公路”，它负责处理和传输大量的数据流量，连接着不同的地区、城市、国家甚至是不同的互联网服务提供商（ISP）。骨干网通常由高速光纤、电缆、卫星等组成，并配备高性能的路由器和交换机，以保证数据在全球范围内高效、可靠地传输。

骨干网的主要特点包括：

1. 高速与高容量：骨干网需要承载大量的流量，通常采用高速的光纤或其他先进的传输技术，以保证大数据量的快速传输。
2. 广泛的覆盖范围：它跨越多个地区，甚至国家，连接着不同的网络，确保全球互联网的互联互通。
3. 低延迟与高稳定性：为了保证数据传输的效率和准确性，骨干网通常采用优质的网络设备和技术，减少传输中的延迟和丢包。

骨干网与接入网的区别包括：

1. 功能不同：骨干网的主要功能是连接不同的网络，处理大量的数据流量，而接入网的主要功能是将终端用户连接到骨干网。

2. 规模与容量：骨干网通常覆盖广泛，承载的流量非常大，网络设备的处理能力也很强。而接入网的规模较小，连接的终端用户较多，但流量和处理能力相对较低。

3. 速度与延迟：由于骨干网采用高速的光纤或其他传输技术，它的速度远高于接入网。此外，骨干网的延迟较低，而接入网的延迟可能较高，尤其是在带宽受限的情况下。

4. 技术差异：骨干网多使用光纤、卫星等高效传输技术，支持大规模的路由和交换设备；接入网则根据不同地区和需求，可能采用光纤、DSL、无线网络等多种技术。

简单来说，骨干网是支撑整个互联网的核心部分，负责处理和传输大量的跨区域流量，而接入网则是将用户连接到互联网的“桥梁”。两者的作用互补，共同保证网络的稳定运行。

## 以铁路运输为比喻

为了更好地理解网络中的接入网和核心网，我们可以借助一个大家都熟悉的比喻——铁路运输。

接入网可以类比为火车站或车站的接驳系统。火车站是乘客进入铁路系统的起点。就像是你从家里出发，必须先到达最近的火车站，然后才能乘坐火车到达更远的目的地。

在网络中，接入网就是接入用户的地方，它通过各种接入方式（如Wi-Fi、光纤、4G/5G等）将用户设备连接到更广泛的网络。每个用户、每个终端设备都通过接入网“上车”，然后把数据通过网络传输到更远的目的地。

核心网可以类比为铁路的主干铁路线路。这些主干铁路是连接不同地区、城市的重要通道，它们承载了大量的火车流量，确保了不同地区之间的连通性。

在网络中，核心网是指负责传输大量数据的高容量网络部分，它连接不同的接入网，保障数据在广阔区域内流动。核心网通常采用高速传输技术，如光纤等，能够承载大量的数据流量，并保证数据的高效交换。

通过铁路运输的比喻，我们可以轻松理解接入网和核心网。接入网就像是我们日常出行的火车站或接驳系统，它负责连接用户与网络；而核心网则像是铁路的主干线路，负责连接不同的地区并传输大量数据流量。无论是通过Wi-Fi、光纤还是5G，我们都在利用这些接入方式来“乘坐”网络数据列车，最终到达目的地。

## 电话交换网的接入网和骨干网

电话交换网通常由电话总局和骨干交换机组成。电话总局的主要作用是接收和管理来自各个用户的电话信号，然后将这些信号发送到骨干交换机进行处理和转接。

具体来说，电话总局负责收集来自用户的电话请求，并将这些请求转发给骨干交换机。骨干交换机的作用则是在长距离的电话业务中起到至关重要的作用，它负责将电话信号从一个地方转接到另一个地方。例如，当你从北京打电话到上海时，骨干交换机就会负责把信号从北京的电话总局传递到上海的电话总局，并确保电话连接成功。

骨干交换机的设计和功能非常重要，因为它们不仅要处理大量的通话请求，还要保证通话质量，确保电话信号能够稳定且清晰地传输到远程地点。这些交换机通常位于网络的骨干区域，通过高速的连接线路将各地的电话服务链接在一起。

长途电话交换主要解决的是跨区域通信的问题。例如，当你从北京打电话到上海时，由于两地之间的电话网络不是直接连接的，就需要通过交换机进行信号转接。这时，电话网络会通过长途交换设备将信号传递到目的地。

如果你在同一个城市或同一个校园内打电话，例如从北京交通大学的一个电话拨打到另一个电话（例如5168号码），这时候就不需要经过长途交换，因为这些电话属于同一个本地交换网络，直接由当地的交换机处理即可。由于这种通话是在本地网络内进行，不涉及跨区域的信号转接，因此通常不需要支付长途费用。这种情况通常适用于校园内部电话、公司内线电话等，它们的通信成本较低，只需要支付本地通信费用。

因此，校园电话或公司内部的电话通话费用较为便宜，因为它们仅仅依赖本地交换系统，不涉及到长途电话的中转和费用。

## 分组交换网的边缘路由器和核心路由器

边缘路由器和核心路由器也是我们常见的两个网络概念。

在现代互联网中，路由器扮演着至关重要的角色。它们通过传递数据包来实现不同网络之间的连接。路由器有两种常见类型：核心路由器和边缘路由器。

1. 核心路由器：核心路由器位于网络的中心，负责处理网络中的大量流量。这些路由器通常具有较强的处理能力，能够高效地转发数据包。它们在网络中处于关键位置，承载着重要的任务，决定着数据的传输效率。网络中多个核心路由器相互连接，形成网络的主干。

2. 边缘路由器：边缘路由器位于网络的边缘，连接着终端用户和核心网络。它们的作用是将用户的流量接入到核心网络，并将核心网络的流量分发到终端用户。边缘路由器通常负责数据的复用和拆解。例如，它可能会将多个用户的流量复用成一个高效的数据流，发送到核心网络中。

边缘路由器的主要作用之一就是根据不同用户的需求，合理分配网络资源。它们将来自多个用户的请求汇聚并进行复用，从而提高网络资源的利用率。

随着物联网（IoT）和智能设备的普及，边缘计算已经成为一个热门的技术趋势。边缘智能指的是在网络的边缘端处理和计算数据，以减少数据传输的延迟和带宽压力。

例如，国家电网已经开始使用边缘智能技术，在变压器等设备中嵌入计算模块。这些模块可以实时处理设备的状态信息，并做出决策。这种边缘计算可以帮助实现智能调度和高效管理，减少对中心服务器的依赖。

## 讨论：你接触过什么接入网？

举个例子，大家在生活中最常用的网络接入方式有哪些？

- 拨号上网：曾经的老式拨号上网可以类比为“电话线路”，它为你提供了最基础的上网接入。
- Wi-Fi：现在常用的Wi-Fi就像是家庭和办公室中的小火车站，它让你可以在家里或者工作场所轻松地“登上网络列车”。
- 光纤通信：光纤就像是现代的高速铁路，它为你提供稳定且快速的上网体验。比如家里安装的光纤宽带就属于这种类型。
- 5G通信：现代的5G通信，犹如新一代的超高速列车，它将带给你更快速的上网体验，特别是在城市和人群密集的地方。
- 有线电视网：虽然它现在逐渐被互联网取代，但有线电视网也是一种特殊的接入网类型，可以将信息从传输线路传送到家庭设备。

## 扩展阅读：中国的骨干网

中国的核心骨干网是由多个大型电信运营商和互联网服务提供商所建设和运营的，它们构成了国家的高速数据传输网络，支撑着全国范围内的数据通信和互联网服务。以下是中国主要的核心骨干网：

- 中国电信骨干网：中国电信作为国内最大的电信运营商之一，其骨干网涵盖了全国范围的通信基础设施。中国电信的骨干网包括了大量的光纤传输线路，覆盖了全国的城市和一些偏远地区。中国电信在国内拥有多个核心数据中心，并通过这些数据中心为用户提供宽带、电话、数据通信等服务。
- 中国联通的骨干网：中国联通的核心骨干网也覆盖了全国范围，主要依靠光纤和高速数据线路进行数据传输。联通的骨干网包括一些重要的互联网交换中心，支持数据传输、云计算、企业专线等服务。中国联通还与其他运营商合作，建立了部分国际骨干网连接，提供跨国通信服务。
- 中国移动的骨干网：中国移动作为全球最大的移动通信运营商之一，其核心骨干网不仅包括传统的通信网络，还涵盖了大量的移动通信基础设施。中国移动的骨干网为全国范围的手机通信和互联网接入提供服务，其网络规模庞大，技术更新迅速。中国移动还通过其骨干网提供宽带服务和企业级通信解决方案。
- 中国教育和科研网（CERNET）：CERNET是中国的教育和科研专用网络，它是中国重要的互联网骨干网之一，连接着全国各大高校和科研机构。CERNET的骨干网提供了高速、稳定的科研和学术数据传输网络，并且是许多国家级科研项目的数据支持平台。
- 中国国际互联网数据传输网（ChinaNet）：中国国际互联网数据传输网是中国互联网与全球其他地区通信的桥梁，主要由中国电信运营。它提供跨境数据传输服务，支持中国与世界各地的网络连接。ChinaNet的骨干网在国际通信中占有重要地位。

总之，中国的核心骨干网由多个大型电信公司和互联网服务提供商共同构成，包括中国电信、中国联通、中国移动、CERNET等。它们通过先进的光纤网络、数据中心和交换机等基础设施，支撑着全国的通信需求，同时与全球互联网互联互通。这些骨干网不仅支持国内的语音通信和数据传输，还在全球互联网通信中发挥着重要作用。

## 接入网和骨干网的流量随机性比较

在网络中，接入网和骨干网都承载着不同的流量类型，而这两者的流量随机性存在一定的区别。

接入网是用户直接与网络连接的部分，比如家里的Wi-Fi、4G/5G网络等。接入网的流量通常是由各个单独用户的使用情况决定的，每个用户的上网需求和流量都是随机的。例如，在某个时刻，可能有些用户在观看视频，有些用户在进行在线游戏，流量需求高低波动很大。这种个体用户流量的随机性通常较高。

由于每个用户的行为差异，这些流量的波动是不可预测的。例如，有些用户在某个时段使用网络，而有些则不使用，形成了一定的波动和随机性。

骨干网是连接不同接入网的核心部分，它承载的是来自多个接入网的流量。不同于接入网的流量，骨干网流量的特点是复用，也就是多个接入网的流量合并到骨干网中进行传输。

在骨干网中，虽然每个接入网的流量可能会有随机波动，但由于这些流量来自于多个接入网，且可能存在一定的负载均衡和流量优化机制，所以经过复用后，整体流量的波动性（即随机性）会比接入网低一些。多用户流量的复用和合并会使得总体流量趋于平稳，因此骨干网的随机性通常低于接入网。

回到问题中提到的“接入网流量和骨干网流量，哪一个的随机性更高？”的思考。

- 接入网的流量随机性较高，因为它是由大量单独用户的行为决定的，每个用户的上网行为在时间上都是随机的，这些行为波动非常大，形成了不确定性。
- 而骨干网的流量随机性较低，因为它是多个接入网流量的合成结果，通过复用和合并，这些不稳定的流量波动被一定程度上平滑化，使得总体流量较为稳定。

假设有1000个用户，每个用户上网的时间和使用需求都是随机的。有些用户在某些时段不使用网络，有些则高强度使用网络。当这些用户的流量经过接入网传输时，其波动性较大，因为用户的行为没有什么规律可言。

但当这些用户的流量汇聚到骨干网后，经过复用、合并，整体流量的波动性会减少。例如，部分用户没有使用网络时，其他用户的流量会“填补”这些空隙，从而减少了整体流量波动的随机性。

接入网的流量随机性更高，因为每个用户的行为和需求是独立且随机的。而骨干网的流量随机性较低，由于多个接入网的流量复用和优化，整体的流量波动被平滑化。

|[Index](./) | [Previous](1-3-packetnet) | [Next](1-5-service-transport) |
