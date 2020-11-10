# Open Cloud-native Game-application Initiative

## What is OCGI?

OCGI (Open Cloud-native Game-application Initiative) is a opensource project created by [Tencent Games](https://game.qq.com) Computing Resources Team, which mainly solves the problems when running and scaling game server on Kubernetes cluster.

Generally speaking, the online multiplayer games such as competitive [FPS](https://en.wikipedia.org/wiki/First-person_shooter)s and [MOBA](https://en.wikipedia.org/wiki/Multiplayer_online_battle_arena)s, require a [dedicated game server](https://en.wikipedia.org/wiki/Game_server#Dedicated_server) which simulating game worlds, and players connect to the server with separate client programs, then playing within it. 

Dedicated game servers are stateful applications that retain the full game simulation in memory. But unlike other stateful applications, such as databases, they have a short lifetime. Rather than running for months or years, a dedicated game server process will exit when a game is over, which usually lasts a few minutes or hours.

The Kubernetes [Statefulset](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/) workload does not manage such applications well. So we developed this project to make game servers runing and scaling better on Kubernetes. 

## Main Features

- Application Interactive Update

  Support application interactive update, delete the replica only after the application confirmed. This is very important for game server, but the Deployment and Statefulset can not support this.

- In-place Update

  Support in-place update image, and the Pod will not be recreated. The local cache data of GameServer can be retained when updating.

- Multiple Pod Auto-scaling Strategies

  Support multiple modes (resource metrics/custom metrics/timing/events/webhook) Pod auto-scaling strategies. In many cases, the application wants to specify the number of service replicas by itself, which can be achieved through webhooks.

- Application-defined Scaling-down Order

  Application can define the scaling-down order of replicas. For example, application can choose the game server replica with least user-accessed to delete. This can not only reduce the cost of scaling-down, but also improve the resource utilization.

- Better Cluster Auto-scaling

  It can be seamlessly integrated with the cluster auto-scaling. Based on the application-confirmed mechanism, can choose any replica to delete after application confirmed when cluster scaling-down.

## Specification

OCGI Workload Specification.

* [GameServer Specification](./specs/gameserver.yaml)
* [Squad Specification](./specs/squad.yaml)
* [GeneralPodAutoscaler Specification](./specs/gpa.yaml)

## Contributing

Welcome to [contribute](./CONTRIBUTING.md) and improve OCGI.

## Community

For any question, welcome to contact us via:

- [Slack](https://ocgi.slack.com)
- [Discussion Forum](https://groups.google.com/g/ocgi)

## License

OCGI is licensed under the Apache License, Version 2.0. See [LICENSE](./LICENSE.md) for the full license text.