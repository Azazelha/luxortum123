/components
  └── RitualIntentForm.js     # форма вибору наміру
  └── PhaseNavigator.js       # логіка фази ритуалу
  └── StageDisplay.js         # показ поточного етапу

/pages
  └── index.js                # домашня, вибір наміру
  └── ritual.js               # основна послідовність ритуалу

/lib
  └── ritualData.js           # структура фаз, етапів

/styles
  └── ritual.css              # стилі для ритуального UI
export const ritual = {
  intent: "Очистити простір від хаосу",
  phases: [
    {
      name: "Підготовка",
      stages: ["Очищення простору", "Медитація", "Встановлення кола"]
    },
    {
      name: "Активація",
      stages: ["Виголошення наміру", "Активація символу", "Візуалізація результату"]
    },
    {
      name: "Завершення",
      stages: ["Подяка", "Закриття кола", "Запис у щоденник"]
    }
  ]
};
// components/RitualIntentForm.js
import React from 'react';

export default function RitualIntentForm({ onStart }) {
  return (
    <div>
      <h1>Оберіть намір</h1>
      <p>Намір: Очистити простір від хаосу</p>
      <button onClick={onStart}>Почати ритуал</button>
    </div>
  );
}
// components/PhaseNavigator.js
import React from 'react';

export default function PhaseNavigator({ currentPhase, totalPhases, onNext }) {
  return (
    <div>
      <p>Фаза {currentPhase + 1} із {totalPhases}</p>
      <button onClick={onNext}>Далі</button>
    </div>
  );
}
// components/StageDisplay.js
import React from 'react';

export default function StageDisplay({ phase, stageIndex }) {
  return (
    <div>
      <h2>{phase.name}</h2>
      <p>{phase.stages[stageIndex]}</p>
    </div>
  );
}
// pages/index.js
import RitualIntentForm from '../components/RitualIntentForm';
import { useRouter } from 'next/router';

export default function Home() {
  const router = useRouter();

  return (
    <div>
      <RitualIntentForm onStart={() => router.push('/ritual')} />
    </div>
  );
}
// pages/ritual.js
import { useState } from 'react';
import { ritual } from '../lib/ritualData';
import PhaseNavigator from '../components/PhaseNavigator';
import StageDisplay from '../components/StageDisplay';

export default function RitualPage() {
  const [phaseIndex, setPhaseIndex] = useState(0);
  const [stageIndex, setStageIndex] = useState(0);

  const currentPhase = ritual.phases[phaseIndex];

  const next = () => {
    if (stageIndex < currentPhase.stages.length - 1) {
      setStageIndex(stageIndex + 1);
    } else if (phaseIndex < ritual.phases.length - 1) {
      setPhaseIndex(phaseIndex + 1);
      setStageIndex(0);
    } else {
      alert("Ритуал завершено!");
    }
  };

  return (
    <div>
      <h1>{ritual.intent}</h1>
      <StageDisplay phase={currentPhase} stageIndex={stageIndex} />
      <PhaseNavigator
        currentPhase={phaseIndex}
        totalPhases={ritual.phases.length}
        onNext={next}
      />
    </div>
  );
}
npm install framer-motion

import { motion } from 'framer-motion';

export default function StageDisplay({ phase, stageIndex }) {
  return (
    <motion.div
      key={stageIndex}
      initial={{ opacity: 0, y: 20 }}
      animate={{ opacity: 1, y: 0 }}
      exit={{ opacity: 0, y: -20 }}
      transition={{ duration: 0.5 }}
    >
      <h2>{phase.name}</h2>
      <p>{phase.stages[stageIndex]}</p>
    </motion.div>
  );
}
npm install react-json-editor-ajrm
import JSONInput from 'react-json-editor-ajrm';
import locale from 'react-json-editor-ajrm/locale/en';

export default function RitualEditor({ data, onChange }) {
  return (
    <JSONInput
      id='ritual_editor'
      placeholder={data}
      locale={locale}
      height='400px'
      width='100%'
      onChange={(e) => {
        if (!e.error) onChange(e.jsObject);
      }}
    />
  );
}
import JSONInput from 'react-json-editor-ajrm';
import locale from 'react-json-editor-ajrm/locale/en';

export default function RitualEditor({ data, onChange }) {
  return (
    <JSONInput
      id='ritual_editor'
      placeholder={data}
      locale={locale}
      height='400px'
      width='100%'
      onChange={(e) => {
        if (!e.error) onChange(e.jsObject);
      }}
    />
  );
import JSONInput from 'react-json-editor-ajrm';
import locale from 'react-json-editor-ajrm/locale/en';

export default function RitualEditor({ data, onChange }) {
  return (
    <JSONInput
      id='ritual_editor'
      placeholder={data}
      locale={locale}
      height='400px'
      width='100%'
      onChange={(e) => {
        if (!e.error) onChange(e.jsObject);
      }}
    />
  );

import Link from 'next/link';

export default function RitualSelection() {
  return (
    <div>
      <h1>Оберіть ритуал</h1>
      <ul>
        <li><Link href="/rituals/cleansing">Очищення</Link></li>
        <li><Link href="/rituals/protection">Захист</Link></li>
      </ul>
    </div>
  );
}
const playSound = (sound) => {
  const audio = new Audio(`/sounds/${sound}.mp3`);
  audio.play();
}; 

