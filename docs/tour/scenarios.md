# Scenarios

A "Scenario" represents a different view of the base Layer.

Each Scenario inherits from its base Layer. Any new objects are added onto all objects in
the base Layer, and you can reference any objects from the base Layer to update them.

Notice that in the below Scenario, we simply turn some objects opacity lower, and define a
new connection to show an alternate view of the deployment diagram.

<div className="embedSVG" dangerouslySetInnerHTML={{__html: require('@site/static/img/generated/animated.svg2')}}></div>

```d2
direction: right

title: {
  label: Normal deployment
  near: bottom-center
  shape: text
  style.font-size: 40
  style.underline: true
}

local: {
  code: {
    icon: https://icons.terrastruct.com/dev/go.svg
  }
}
local.code -> github.dev: commit

github: {
  icon: https://icons.terrastruct.com/dev/github.svg
  dev
  master: {
    workflows
  }

  dev -> master.workflows: merge trigger
}

github.master.workflows -> aws.builders: upload and run

aws: {
  builders -> s3: upload binaries
  ec2 <- s3: pull binaries

  builders: {
    icon: https://icons.terrastruct.com/aws/Developer%20Tools/AWS-CodeBuild_light-bg.svg
  }
  s3: {
    icon: https://icons.terrastruct.com/aws/Storage/Amazon-S3-Glacier_light-bg.svg
  }
  ec2: {
    icon: https://icons.terrastruct.com/aws/_Group%20Icons/EC2-instance-container_light-bg.svg
  }
}

local.code -> aws.ec2: {
  style.opacity: 0.0
}

scenarios: {
  hotfix: {
    title.label: Hotfix deployment
    local.code -> github.dev: {
      style.stroke: "#ca052b"
      style.opacity: 0.1
    }

    github: {
      dev: {
        style.opacity: 0.1
      }
      master: {
        workflows: {
          style.opacity: 0.1
        }
        style.opacity: 0.1
      }

      dev -> master.workflows: {
        style.opacity: 0.1
      }
      style.opacity: 0.1
      style.fill: "#ca052b"
    }

    github.master.workflows -> aws.builders: {
      style.opacity: 0.1
    }

    local.code -> aws.ec2: {
      style.opacity: 1
      style.stroke-dash: 5
      style.stroke: "#167c3c"
    }
  }
}
```
