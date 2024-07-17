% Create an ImecDataset pointing at a specific
>> channelMapFile = 'neuropixPhase3A_kilosortChanMap.mat';
>> imec = Neuropixel.ImecDataset('/data/raw_datasets/neuropixel_01.imec.ap.bin', 'channelMap', channelMapFile);

ImecDataset with properties:

             pathRoot: '/data/raw_datasets'
             fileStem: 'neuropixel_01'
         creationTime: 7.3722e+05
            nChannels: 385
           fileTypeAP: 'ap'
           nSamplesAP: 112412208
           nSamplesLF: 0
                 fsAP: 30000
                 fsLF: NaN
     highPassFilterHz: 300
               apGain: 500
              apRange: [-0.6000 0.6000]
               lfGain: 250
              lfRange: [-0.6000 0.6000]
              adcBits: 10
           channelMap: [1×1 Neuropixel.ChannelMap]
     syncChannelIndex: 385
         syncInAPFile: 1
          badChannels: [3×1 double]
         syncBitNames: [16×1 string]
              syncRaw: []
       bytesPerSample: 2
                hasAP: 0
                hasLF: 0
       channelMapFile: '~/npl/neuropixel-utils/map_files/neuropixPhase3A_kilosortChanMap.mat'
       mappedChannels: [384×1 double]
      nChannelsMapped: 384
    connectedChannels: [374×1 double]
   nChannelsConnected: 374
         goodChannels: [371×1 double]
        nGoodChannels: 371
           channelIdx: [384×1 double]
         channelNames: [385×1 string]
   channelNamesPadded: [385×1 string]
            nSyncBits: 16
        syncBitsNamed: [0×1 double]
      creationTimeStr: '08-Jun-2018 12:09:07'
          apScaleToUv: 2.3438
          lfScaleToUv: 2.3438

% Mark individual channels as bad based on RMS voltage
>> rmsBadChannels = imec.markBadChannelsByRMS('rmsRange', [3 100]);

% Specify names for the individual bits in the sync channel
>> imec.setSyncBitNames([1 2 3], {'trialInfo', 'trialStart', 'stim'});

% Save the bad channels and Sync bit names to the .imec.ap.meta file so they are loaded next time
>> imec.writeModifiedAPMeta();

% Perform common average referencing on the file and save the results to a new location
>> cleanedPath = '/data/cleaned_datasets/neuropixel_01.imec.ap.bin';
>> extraMeta = struct();
>> extraMeta.commonAverageReferenced = true;
>> fnList = {@Neuropixel.DataProcessFn.commonAverageReference};
>> imec = imec.saveTransformedDataset(cleanedPath, 'transformAP', fnList, 'extraMeta', extraMeta);

% Sym link the cleaned dataset into a separate directory for Kilosort2
>> ksPath = '/data/kilosort/neuropixel_01.imec.ap.bin';
>> imec = imec.symLinkAPIntoDirectory(ksPath);

% Inspect the raw IMEC traces
>> imec.inspectAP_timeWindow([200 201]); % 200-201 seconds into the recording