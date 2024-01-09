# `dotnet publish` Size Comparisons

`dotnet publish` options produce production apps in various configrations. This analysis looks at the size differences.

## Linux

![image](https://github.com/richlander/dotnet-publish-size-comparisons/assets/2608468/6c3d19b0-8f4e-436b-a763-a7935d4958c3)

The following `dotnet publish` commands were run on Linux and measured with with `du -h -d 1`.

| Template | Flavor | Size (MB) | Notes   | Command |
| -------- | ------ | ----------| ------- | ------- |
| console  | FDD    | 0.108       | |  `dotnet publish projects/console/ -o results/console-fdd` |
| console  | SCD    | 72       | |  `dotnet publish projects/console/ --sc -o results/console-scd` |
| console  | SCD-Trimmed    | 20       | |  `dotnet publish projects/console/ -p:PublishTrimmed=true -o results/console-scd-trimmed` |
| console  | NAOT    | 1.6       | |  `dotnet publish projects/console/ -p:PublishAot=true -p:CopyOutputSymbolsToPublishDirectory=false -o results/console-naot` |
| worker  | FDD    | 2.3       | |  `dotnet publish projects/worker/ -o results/worker-fdd` |
| worker  | SCD    | 73       | |  `dotnet publish projects/worker/ --sc -o results/worker-scd` |
| worker  | SCD-Trimmed    | 22       | |  `dotnet publish projects/worker/ -p:PublishTrimmed=true -o results/worker-scd-trimmed` |
| worker  | NAOT    | 5.1      | |  `dotnet publish projects/worker/ -p:PublishAot=true -p:CopyOutputSymbolsToPublishDirectory=false -o results/worker-nao` |
| webapi  | FDD    | 3.8       | |  `dotnet publish projects/webapi -o results/webapi-fdd` |
| webapi  | SCD    | 100       | |  `dotnet publish projects/webapi --sc -o results/webapi-scd` |
| webapi  | SCD-Trimmed    | 30  | 6 trimming warnings / throws at runtime |   `dotnet publish projects/webapi -p:PublishTrimmed=true -o results/webapi-scd-trimmed` |
| webapiaot  | NAOT    | 10      | |  `dotnet publish projects/webapiaot/ -p:PublishAot=true -p:CopyOutputSymbolsToPublishDirectory=false -o results/webapiaot-naot` |
| grpc  | FDD    | 1.2       | |  `dotnet publish projects/grpc/ -o results/grpc-fdd` |
| grpc  | SCD    | 97       | |  `dotnet publish projects/grpc/ --sc -o results/grpc-scd` |
| grpc  | SCD-Trimmed    | 27       | |  `dotnet publish projects/grpc/ -p:PublishTrimmed=true -o results/grpc-scd-trimmed` |
| grpc  | NAOT    | 18       | |  `dotnet publish projects/grpc/ -p:PublishAot=true -p:CopyOutputSymbolsToPublishDirectory=false -o results/grpc-naot` |
| web  | FDD    | 0.128       | |  `dotnet publish projects/web/ -o results/web-fdd` |
| web  | SCD    | 96       | |  `dotnet publish projects/web/ --sc -o results/web-scd` |
| web  | SCD-Trimmed    | 26       | |  `dotnet publish projects/web/ -p:PublishTrimmed=true -o results/web-scd-trimmed` |
| web  | NAOT    | 17       | |  `dotnet publish projects/web/ -p:PublishAot=true -p:CopyOutputSymbolsToPublishDirectory=false -o results/web-naot` |
| mvc  | FDD    | 8.2       | |  `dotnet publish projects/mvc/ -o results/mvc-fdd` |
| mvc  | SCD    | 104       | |  `dotnet publish projects/mvc/ --sc -o results/mvc-scd` |
| mvc  | SCD-Trimmed    | 38       | 8 warnings / core dumps |  `dotnet publish projects/mvc/ -p:PublishTrimmed=true -o results/mvc-scd-trimmed` |
| mvc  | NAOT    | 33       | 18 warnings / core dumps |  `dotnet publish projects/web/ -p:PublishAot=true -p:CopyOutputSymbolsToPublishDirectory=false -o results/web-naot` |
| blazor | FDD    | 0.784       | |  `dotnet publish projects/blazor/ -o results/blazor-fdd` |
| blazor | SCD    | 97       | |  `dotnet publish projects/blazor/ --sc -o results/blazor-scd` |
| blazor | SCD-Trimmed    | 31       | 11 warnings / fails (no error) |  `dotnet publish projects/blazor/ -p:PublishTrimmed=true -o results/blazor-scd-trimmed` |
| blazor | NAOT    | 26       | 18 warnings / fails (no error) |  `dotnet publish projects/blazor/ -p:PublishAot=true -p:CopyOutputSymbolsToPublishDirectory=false -o results/blazor-naot` |

Notes:

- The "Flavor" terms are [.NET Deployment modes](https://learn.microsoft.com/en-us/dotnet/core/deploying/).