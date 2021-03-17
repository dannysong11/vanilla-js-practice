```javascript
/*
 * Scenario:
 *
 * You are receiving a list of show/input metadata coming from our system.
 * The data structure is expected as the exampleInputs below.
 *
 * the input has to have the following mandatory fields (as asset):
 * asset.id, asset.title, asset.description, asset.broadcastStartTime asset.duration, asset.image
 *
 * Inputs don't have to have an match object, but if an property has a match object,
 * the match object has to have the following mandatory fields:
 * option.id,
 * option.homeTeam.id, option.homeTeam.name, option.homeTeam.image,
 * option.awayTeam.id, option.awayTeam.name, option.awayTeam.image,
 *
 *
 * Requirement:
 * Create an software component in JavaScript which will take the exampleInputs as input and output a new list which will:
 * 1. filter out any asset or match that missing mandatory fields.
 * 2. output asset list should not include any optional fields; NOTE: if an asset has match object,
 *    the output asset list should include the match object unless the match object is missing any mandatory field
 * 3. create broadcastEndTime for each of the asset. It's value should be broadcastStartTime + duration in ISO8601 format
 *    (same format as broadcastStartTime)
 * 4. replace img.domainone.com/cms to img.domaintwo.com for all image url
 * 5. sort the output asset list by broadcastStartTime
 */

exampleInputs = [
  {
    id: '100001',
    title: 'asset 1',
    description: 'this is asset 1',
    broadcastStartTime: '2020-01-16T02:48:28Z',
    duration: 1000,  // in seconds
    image: 'https://img.domainone.com/cms/assets/100001.jpg',
    option: {
      id: 'matchId200001',
      homeTeam: {
        id: 'teamId00001',
        name: 'team 000001',
        image: 'https://img.domainone.com/cms/teams/100001.jpg',
        address: "team 00001 address"
      },
      awayTeam: {
        id: 'teamId00002',
        name: 'team 000002',
        image: 'https://img.domainone.com/cms/teams/100002.jpg'
      }
    },
    tags: ['tag1', 'tag2'],
    updateAt: '2019-01-16T02:48:28Z',
    type: 'minimatch'
  },
  {
    id: '100002',
    title: 'asset 2',
    description: 'this is asset 2',
    image: 'https://img.domainone.com/cms/assets/100002.jpg',
    broadcastStartTime: '2018-01-16T02:48:28Z',
    duration: 60000,
    tags: ['tag1', 'tag2'],
    updateAt: '2019-01-16T02:48:28Z',
    type: 'minimatch'
  },
  {
    id: '100003',
    image: 'https://img.domainone.com/cms/assets/100003.jpg',
    broadcastStartTime: '2018-01-16T02:48:28Z',
    duration: 60000,
    tags: ['tag1', 'tag2'],
    updateAt: '2019-01-16T02:48:28Z',
    type: 'minimatch'
  },
  {
    id: '100004',
    title: 'asset 4',
    description: 'this is asset 4',
    broadcastStartTime: '2022-01-16T02:48:28Z',
    duration: 81000,
    image: 'https://img.domainone.com/cms/assets/100004.jpg',
    match: {
      homeTeam: {
        id: 'teamId00006',
        image: 'https://img.domainone.com/cms/teams/100006.jpg'
      },
      awayTeam: {
        id: 'teamId00009',
        name: 'team 000009',
        image: 'https://img.domainone.com/cms/teams/100009.jpg'
      }
    },
    tags: ['tag1', 'tag2'],
    updateAt: '2019-01-16T02:48:28Z',
    type: 'minimatch'
  }
];

exampleOutputs = [
  {
    id: '100002',
    title: 'asset 2',
    description: 'this is asset 2',
    image: 'https://img.domaintwo.com/assets/100002.jpg',
    broadcastStartTime: '2018-01-16T02:48:28Z',
    duration: 60000,
    broadcastEndTime: '2018-01-16T07:28:28Z', /* broadcastStartTime + 1000 seconds */
  },
  {
    id: '100001',
    title: 'asset 1',
    description: 'this is asset 1',
    broadcastStartTime: '2020-01-16T02:48:28Z',
    duration: 1000,  // in seconds
    broadcastEndTime: '2020-01-16T03:05:08Z', /* broadcastStartTime + 1000 seconds */
    image: 'https://img.domaintwo.com/assets/100001.jpg',
    match: {
      id: 'matchId200001',
      homeTeam: {
        id: 'teamId00001',
        name: 'team 000001',
        image: 'https://img.domaintwo.com/teams/100001.jpg'
        /* optional fields (address) got removed */
      },
      awayTeam: {
        id: 'teamId00002',
        name: 'team 000002',
        image: 'https://img.domaintwo.com/teams/100002.jpg'
      }
    }
  },
  {
    id: '100004',
    title: 'asset 4',
    description: 'this is asset 4',
    image: 'https://img.domaintwo.com/assets/100004.jpg',
    broadcastStartTime: '2022-01-16T02:48:28Z',
    duration: 81000
    broadcastEndTime: '2022-01-17T01:18:28Z', 
  }
];
```
